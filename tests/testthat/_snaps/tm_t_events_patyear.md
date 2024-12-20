# template_events_patyear generates standard expressions

    Code
      res
    Output
      $data
      {
          anl <- adaette
          anl <- anl %>% dplyr::mutate(ARMCD = droplevels(ARMCD))
          arm_levels <- levels(anl[["ARMCD"]])
          adsl <- adsl %>% dplyr::filter(ARMCD %in% arm_levels)
          adsl <- adsl %>% dplyr::mutate(ARMCD = droplevels(ARMCD))
          anl <- df_explicit_na(anl, na_level = "<Missing>")
          adsl <- df_explicit_na(adsl, na_level = "<Missing>")
      }
      
      $layout
      lyt <- rtables::basic_table(show_colcounts = TRUE, title = "Event Rates Adjusted for Patient-Years by Time to First Occurrence of any Adverse Event", 
          main_footer = "CI Method: Normal (rate)") %>% rtables::split_cols_by(var = "ARMCD") %>% 
          rtables::add_overall_col(label = "All Patients") %>% estimate_incidence_rate(vars = "AVAL", 
          n_events = "n_events", control = control_incidence_rate(conf_level = 0.95, 
              conf_type = "normal", input_time_unit = "year", num_pt_year = 100))
      
      $table
      {
          table <- rtables::build_table(lyt = lyt, df = anl, alt_counts_df = adsl)
      }
      

# template_events_patyear generates right expressions with non-default

    Code
      res
    Output
      $data
      {
          anl <- adaette
          adsl <- adsl %>% dplyr::mutate(ARM = droplevels(ARM))
          arm_levels <- levels(adsl[["ARM"]])
          anl <- anl %>% dplyr::mutate(ARM = factor(ARM, levels = arm_levels))
          anl <- df_explicit_na(anl, na_level = "<Missing>")
          adsl <- df_explicit_na(adsl, na_level = "<Missing>")
      }
      
      $layout
      lyt <- rtables::basic_table(show_colcounts = TRUE, title = "Event Rates Adjusted for Patient-Years by Time to First Occurrence of any Adverse Event", 
          main_footer = "CI Method: Normal (rate)") %>% rtables::split_cols_by(var = "ARM") %>% 
          estimate_incidence_rate(vars = "AVAL", n_events = "n_events", 
              control = control_incidence_rate(conf_level = 0.95, conf_type = "normal", 
                  input_time_unit = "year", num_pt_year = 100))
      
      $table
      {
          table <- rtables::build_table(lyt = lyt, df = anl, alt_counts_df = adsl)
      }
      

# template_events_patyear generates right expressions with non-default controls

    Code
      res
    Output
      $data
      {
          anl <- adaette
          anl <- anl %>% dplyr::mutate(ARM = droplevels(ARM))
          arm_levels <- levels(anl[["ARM"]])
          adsl <- adsl %>% dplyr::filter(ARM %in% arm_levels)
          adsl <- adsl %>% dplyr::mutate(ARM = droplevels(ARM))
          anl <- anl %>% dplyr::mutate(SEX = droplevels(SEX))
          arm_levels <- levels(anl[["SEX"]])
          adsl <- adsl %>% dplyr::filter(SEX %in% arm_levels)
          adsl <- adsl %>% dplyr::mutate(SEX = droplevels(SEX))
          anl <- df_explicit_na(anl, na_level = "<Missing>")
          adsl <- df_explicit_na(adsl, na_level = "<Missing>")
      }
      
      $layout
      lyt <- rtables::basic_table(show_colcounts = TRUE, title = "Event Rates Adjusted for Patient-Years by Time to First Occurrence of any Adverse Event", 
          main_footer = "CI Method: Exact") %>% rtables::split_cols_by(var = "ARM") %>% 
          rtables::split_cols_by("SEX", split_fun = drop_split_levels) %>% 
          rtables::add_overall_col(label = "All Patients") %>% estimate_incidence_rate(vars = "AVAL", 
          n_events = "n_events", control = control_incidence_rate(conf_level = 0.9, 
              conf_type = "exact", input_time_unit = "month", num_pt_year = 80))
      
      $table
      {
          table <- rtables::build_table(lyt = lyt, df = anl, alt_counts_df = adsl)
      }
      

