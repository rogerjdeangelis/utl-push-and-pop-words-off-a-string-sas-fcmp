# utl-push-and-pop-words-off-a-string-sas-fcmp
Push and pop words off a string sas fcmp
    Push and pop words off a string sas fcmp                                                                        
                                                                                                                    
     Three solutions                                                                                                
                                                                                                                    
          a. scan substr                                                                                            
             Kurt Bremser                                                                                           
             https://communities.sas.com/t5/user/viewprofilepage/user-id/11562                                      
          b. fcmp (pop off first word)                                                                              
          c. fcmp with common storage concept and first,last and middle strings                                     
             middle string can be multiple words                                                                    
                                                                                                                    
    github                                                                                                          
    https://tinyurl.com/y33y33yq                                                                                    
    https://github.com/rogerjdeangelis/utl-push-and-pop-words-off-a-string-sas-fcmp                                 
                                                                                                                    
    SAS Form                                                                                                        
    https://tinyurl.com/y2eh6mxb                                                                                    
    https://communities.sas.com/t5/SAS-Programming/Delete-first-word-before-first-space/m-p/693090                  
                                                                                                                    
    Related github                                                                                                  
    github                                                                                                          
    https://tinyurl.com/ycqntnuz                                                                                    
    https://github.com/rogerjdeangelis/utl-general-data-input-method-that-pops-words-out-of-a-sentence              
                                                                                                                    
                                                                                                                    
    Eight related solutions by five expert SAS programmers (New string with everything AFTER the first space)       
                                                                                                                    
    github                                                                                                          
    https://tinyurl.com/y2vx2fr4                                                                                    
    https://github.com/rogerjdeangelis/utl-remove-the-first-and-last-word-from-hyphenated-list                      
                                                                                                                    
    also                                                                                                            
    SAS forum                                                                                                       
    https://tinyurl.com/yydlxqmu                                                                                    
    https://communities.sas.com/t5/SAS-Programming/How-to-remove-the-prefix-and-suffix-at-one-step/m-p/557169       
                                                                                                                    
    /*                   _                                                                                          
    (_)_ __  _ __  _   _| |_                                                                                        
    | | `_ \| `_ \| | | | __|                                                                                       
    | | | | | |_) | |_| | |_                                                                                        
    |_|_| |_| .__/ \__,_|\__|                                                                                       
            |_|                                                                                                     
    */                                                                                                              
                                                                                                                    
    data have;                                                                                                      
    input brand $50.;                                                                                               
    cards4;                                                                                                         
    CITROEN C3 AIRCROSS                                                                                             
    DS3 CROSSBACK E-TENSE                                                                                           
    OPEL GRANDLAND X                                                                                                
    ;;;;                                                                                                            
    run;quit;                                                                                                       
                                                                                                                    
    WORK.HAVE total obs=3                                                                                           
                                                                                                                    
    Obs            BRAND                                                                                            
                                                                                                                    
     1     CITROEN C3 AIRCROSS                                                                                      
     2     DS3 CROSSBACK E-TENSE                                                                                    
     3     OPEL GRANDLAND X                                                                                         
                                                                                                                    
    /*           _               _                                                                                  
      ___  _   _| |_ _ __  _   _| |_                                                                                
     / _ \| | | | __| `_ \| | | | __|                                                                               
    | (_) | |_| | |_| |_) | |_| | |_                                                                                
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                               
                    |_|                        _         _                                                          
      __ _     ___  ___ __ _ _ __    ___ _   _| |__  ___| |_ _ __                                                   
     / _` |   / __|/ __/ _` | `_ \  / __| | | | `_ \/ __| __| `__|                                                  
    | (_| |_  \__ \ (_| (_| | | | | \__ \ |_| | |_) \__ \ |_| |                                                     
     \__,_(_) |___/\___\__,_|_| |_| |___/\__,_|_.__/|___/\__|_|                                                     
     _         __                                                                                                   
    | |__     / _| ___ _ __ ___  _ __                                                                               
    | `_ \   | |_ / __| `_ ` _ \| `_ \                                                                              
    | |_) |  |  _| (__| | | | | | |_) |                                                                             
    |_.__(_) |_|  \___|_| |_| |_| .__/                                                                              
                                |_|                                                                                 
    */                                                                                                              
                                                                                                                    
     WORK.WANT total obs=3                                                                                          
                                                                                                                    
        MAKE       MODEL                                                                                            
                                                                                                                    
        CITROEN    C3 AIRCROSS                                                                                      
        DS3        CROSSBACK E-TENSE                                                                                
        OPEL       GRANDLAND X                                                                                      
                                                                                                                    
    /*                             __ _          _     _           _                                                
      ___     _ __   ___  _ __    / _(_)_ __ ___| |_  | | __ _ ___| |_                                              
     / __|   | `_ \ / _ \| `_ \  | |_| | `__/ __| __| | |/ _` / __| __|                                             
    | (__ _  | |_) | (_) | |_) | |  _| | |  \__ \ |_  | | (_| \__ \ |_                                              
     \___(_) | .__/ \___/| .__/  |_| |_|_|  |___/\__| |_|\__,_|___/\__|                                             
             |_|         |_|                                                                                        
    */                                                                                                              
                                                                                                                    
    WORK.WANT total obs=3                                                                                           
                                                                                                                    
     POP1ST     MIDDLE      POPLST                                                                                  
                                                                                                                    
     CITROEN    C3          AIRCROSS                                                                                
     DS3        CROSSBACK   E-TENSE                                                                                 
     OPEL       GRANDLAND   X                                                                                       
                                                                                                                    
                                                                                                                    
    /*         _       _   _                                                                                        
     ___  ___ | |_   _| |_(_) ___  _ __  ___                                                                        
    / __|/ _ \| | | | | __| |/ _ \| `_ \/ __|                                                                       
    \__ \ (_) | | |_| | |_| | (_) | | | \__ \                                                                       
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|___/  _         _                                                          
      __ _     ___  ___ __ _ _ __    ___ _   _| |__  ___| |_ _ __                                                   
     / _` |   / __|/ __/ _` | `_ \  / __| | | | `_ \/ __| __| `__|                                                  
    | (_| |_  \__ \ (_| (_| | | | | \__ \ |_| | |_) \__ \ |_| |                                                     
     \__,_(_) |___/\___\__,_|_| |_| |___/\__,_|_.__/|___/\__|_|                                                     
    */                                                                                                              
                                                                                                                    
    data want;                                                                                                      
      set have;                                                                                                     
      make = scan(brand,1);                                                                                         
      call scan(brand,1,p,l);                                                                                       
      model = substr(brand,l+2);                                                                                    
      drop p l brand;                                                                                               
    run;quit;                                                                                                       
                                                                                                                    
    /*                                                                                                              
     _         __                                                                                                   
    | |__     / _| ___ _ __ ___  _ __                                                                               
    | `_ \   | |_ / __| `_ ` _ \| `_ \                                                                              
    | |_) |  |  _| (__| | | | | | |_) |                                                                             
    |_.__(_) |_|  \___|_| |_| |_| .__/                                                                              
                                |_|                                                                                 
    *    * pop words off the beginning or end of a string and return reduced string;  
    * somewhat dataed - new SAS function may be better;                          
                                                                                 
    options cmplib=work.functions;                                               
    proc fcmp outlib=work.functions.temp;                                        
    Subroutine utl_pop(string $,word $,action $);                                
        outargs word, string;                                                    
        length word $4096;                                                       
        select (upcase(action));                                                 
          when ("LAST") do;                                                      
            call scan(string,-1,_action,_length,' ');                            
            word=substr(string,_action,_length);                                 
            string=substr(string,1,_action-1);                                   
          end;                                                                   
                                                                                 
          when ("FIRST") do;                                                     
            call scan(string,1,_action,_length,' ');                             
            word=substr(string,_action,_length);                                 
            string=substr(string,_action + _length);                             
          end;                                                                   
                                                                                 
          otherwise put "ERROR: Invalid action";                                 
                                                                                 
        end;                                                                     
    endsub;                                                                      
    run;quit;                                                                    
/     

    
                                                                                                                    
    data want(rename=brand=model);                                                                                  
    retain make "               ";                                                                                  
    set have;                                                                                                       
    call utl_pop(brand,make,"FIRST");                                                                               
    run;quit;                                                                                                       
                                                                                                                    
    /*         __ _          _     _           _               _     _     _ _                                      
      ___     / _(_)_ __ ___| |_  | | __ _ ___| |_   _ __ ___ (_) __| | __| | | ___                                 
     / __|   | |_| | `__/ __| __| | |/ _` / __| __| | `_ ` _ \| |/ _` |/ _` | |/ _ \                                
    | (__ _  |  _| | |  \__ \ |_  | | (_| \__ \ |_  | | | | | | | (_| | (_| | |  __/                                
     \___(_) |_| |_|_|  |___/\__| |_|\__,_|___/\__| |_| |_| |_|_|\__,_|\__,_|_|\___|                                
    */                                                                                                              
                                                                                                                    
    data want(rename=brand=middle);                                                                                 
       retain pop1st popLst "          ";  * you can use a length statement here;                                   
       set have;                                                                                                    
       call utl_pop(brand,pop1st,"FIRST");                                                                          
       call utl_pop(brand,popLst,"LAST");                                                                           
    run;quit;                                                                                                       
                                                                                                                    
                                                                                                                    
                                                                 
                                                  
    /*                                               _                                                              
      ___ ___  _ __ ___  _ __ ___   ___  _ __    ___| |_ ___  _ __ __ _  __ _  ___                                  
     / __/ _ \| `_ ` _ \| `_ ` _ \ / _ \| `_ \  / __| __/ _ \| `__/ _` |/ _` |/ _ \                                 
    | (_| (_) | | | | | | | | | | | (_) | | | | \__ \ || (_) | | | (_| | (_| |  __/                                 
     \___\___/|_| |_| |_|_| |_| |_|\___/|_| |_| |___/\__\___/|_|  \__,_|\__, |\___|                                 
                                                                        |___/                                       
    */                                                                                                              
    * this extracts the first and the last words in a string;                                                       
                                                                                                                    
    * As a side note I find the concept of common storage to be useful here.                                        
    It is also useful with 'DOSUBL";                                                                                
                                                                 
                                                  
    %macro commonChar(var,size)/                                                                                    
          des="decare the name and size of a variable to share with FCMP";                                          
      length &var $&size;                                                                                           
      retain &var " ";                                                                                              
    %mend commonChar;                                                                                               
                                                                                                                    
    data want;                                                                                                      
    %commonChar(pop1st popLst,32);                                                                                  
    set have;                                                                                                       
    call utl_pop(brand,pop1st,"FIRST");                                                                             
    call utl_pop(brand,popLst,"LAST");                                                                              
    run;quit;                                                                                                       
                                                                                                                    
