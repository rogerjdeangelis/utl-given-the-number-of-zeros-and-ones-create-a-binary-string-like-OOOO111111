# utl-given-the-number-of-zeros-and-ones-create-a-binary-string-like-OOOO111111
Given the number of zeros and ones create a binary string like OOOO111111

     Given the number of zeros and ones create a binary string like OOOO111111                                                          
                                                                                                                                        
          Three Solutions                                                                                                               
                                                                                                                                        
             1. datastep variable string (0,0,0,0,1,1,1,1,1,1)                                                                          
             2. DOSUBL at macro string  (0,0,0,0,1,1,1,1,1,1)                                                                           
             3. Macro string (0,0,0,0,1,1,1,1,1,1)                                                                                      
                                                                                                                                        
                                                                                                                                        
        github                                                                                                                          
        https://tinyurl.com/yxjtr6yv                                                                                                    
        https://github.com/rogerjdeangelis/utl-given-the-number-of-zeros-and-ones-create-a-binary-string-like-OOOO111111/tree/master    
                                                                                                                                        
                                                                                                                                        
        StackOverflow                                                                                                                   
        https://tinyurl.com/y3xk9863                                                                                                    
        https://stackoverflow.com/questions/55974241/how-to-create-a-dynamic-string-in-sas  
        
     _ __   _____      __                                                        
    | '_ \ / _ \ \ /\ / /                                                        
    | | | |  __/\ V  V /                                                         
    |_| |_|\___| \_/\_/                                                          
                                                                                 
                                                                                 
    Clever additions by Bart, Max, and Paul                                              
                                                                                 
    Paul Dorfman <sashole@bellsouth.net>                                         
    May 3, 2019, 8:53 PM (8 hours ago)                                           
                                                                                 
    Roger,                                                                       
                                                                                 
    I don't see how your method can be significantly improved.                   
    But I find interesting that a string with n0 consecutive ones followed       
    by n1 consecutive zeros can be generated using the expression:               
                                                                                 
      putn (2 ** n1 - 1, cats ("binary", n0 + n1, "."))                          
                                                                                 
    Then repeated TRANWRDs can be applied to get what you want, for example:     
                                                                                 
    data _null_ ;                                                                
      retain n0 4 n1 6 ;                                                         
      length str $ 21 ;                                                          
      str = cats ("(",tranwrd(tranwrd(tranwrd(putn(2**n1-1                       
         ,cats("binary",n0+n1,".")),"1",",1"),"0","0,"),",,",","),")") ;         
      put str= ;                                                                 
    run ;                                                                        
                                                                                 
    I freely admit that the resulting expression is, uh, a bit hairy.            
                                                                                 
    Best regards                                                                 
                                                                                 
                                                                                 
    Yinglin (Max) Wu yinglinwu@gmail.com                                         
                                                                                 
    Using binary format ... Just for fun. :)                                     
                                                                                 
    %let n0=5;                                                                   
    %let n1=10;                                                                  
    %put %sysfunc(putn(%eval(2**&n1-1), binary%eval(&n0+&n1).));                 
                                                                                 
    Max                                                                          
                                                                                 
    Bartosz Jablonski                                      
    yabwon@gmail.com                                       
                                                           
    Hi Roger,                                              
                                                           
    I think we can also use (in)famous cats() function     
    and a temporary array - in case strings get bigger;    
                                                           
    all the best                                           
    Bart                                                   
                                                           
                                                           
    %let n0=128;                                           
                                                           
    %let n1=128;                                           
                                                           
    data _null_;                                           
      array t[%eval(&n0+&n1)] (&n0*0 &n1*1);               
      length res $ %eval(&n0+&n1);                         
      res = cats(of t[*]);                                 
      put res=;                                            
    run;                                                   
                                                                             
                                                                                                                             
        *_                   _                                                                                                          
        (_)_ __  _ __  _   _| |_                                                                                                        
        | | '_ \| '_ \| | | | __|                                                                                                       
        | | | | | |_) | |_| | |_                                                                                                        
        |_|_| |_| .__/ \__,_|\__|                                                                                                       
                |_|                                                                                                                     
        ;                                                                                                                               
                                                                                                                                        
           Number of Zeoes  = 4                                                                                                         
           Number of ones   =6  (also length of string - 4);                                                                            
                                                                                                                                        
        *            _               _                                                                                                  
          ___  _   _| |_ _ __  _   _| |_                                                                                                
         / _ \| | | | __| '_ \| | | | __|                                                                                               
        | (_) | |_| | |_| |_) | |_| | |_                                                                                                
         \___/ \__,_|\__| .__/ \__,_|\__|                                                                                               
                        |_|                                                                                                             
        ;                                                                                                                               
                                                                                                                                        
                                                                                                                                        
        1. datastep variable string (0,0,0,0,1,1,1,1,1,1)                                                                               
                                                                                                                                        
                                                                                                                                        
        Up to 40 obs WORK.ZROONE total obs=1                                                                                            
                                                                                                                                        
        Obs    ZRO    ONE           ZROONE                                                                                              
                                                                                                                                        
         1      4      6     (0,0,0,0,1,1,1,1,1,1)                                                                                      
                                                                                                                                        
                                                                                                                                        
                                                                                                                                        
        2. DOSUBL at macro string  (0,0,0,0,1,1,1,1,1,1)                                                                                
                                                                                                                                        
        %put &=xroOne                                                                                                                   
                                                                                                                                        
           ZROONE=(0,0,0,0,1,1,1,1,1,1)                                                                                                 
                                                                                                                                        
                                                                                                                                        
                                                                                                                                        
        3. Macro string (0,0,0,0,1,1,1,1,1,1)                                                                                           
                                                                                                                                        
        %put &=xroOne                                                                                                                   
                                                                                                                                        
           ZROONE=(0,0,0,0,1,1,1,1,1,1)                                                                                                 
                                                                                                                                        
                                                                                                                                        
        *          _       _   _                                                                                                        
         ___  ___ | |_   _| |_(_) ___  _ __  ___                                                                                        
        / __|/ _ \| | | | | __| |/ _ \| '_ \/ __|                                                                                       
        \__ \ (_) | | |_| | |_| | (_) | | | \__ \                                                                                       
        |___/\___/|_|\__,_|\__|_|\___/|_| |_|___/                                                                                       
                                                                                                                                        
        ;                                                                                                                               
                                                                                                                                        
                                                                                                                                        
    ***************************************************                                                                                 
    1. datastep variable string (0,0,0,0,1,1,1,1,1,1)                                                                                   
    ***************************************************                                                                                 
                                                                                                                                        
      data zroOne;                                                                                                                      
                                                                                                                                        
         Zro = 4;                                                                                                                       
         One = 6;                                                                                                                       
                                                                                                                                        
         zroOne=cats("(",repeat("0,",Zro-1),repeat("1,",one-2),"1)");                                                                   
                                                                                                                                        
      run;quit;                                                                                                                         
                                                                                                                                        
                                                                                                                                        
                                                                                                                                        
    ************************************************                                                                                    
    2. DOSUBL at macro string  (0,0,0,0,1,1,1,1,1,1)                                                                                    
    *************************************************                                                                                   
                                                                                                                                        
      %symdel zroOne / nowarn; * just in case;                                                                                          
                                                                                                                                        
      %let rc=%sysfunc(dosubl('                                                                                                         
         data zroOne;                                                                                                                   
                                                                                                                                        
            Zro = 4;                                                                                                                    
            One = 6;                                                                                                                    
                                                                                                                                        
            zroOne=cats("(",repeat("0,",Zro-1),repeat("1,",one-2),"1)");                                                                
            call symputx("zroOne",zroOne);                                                                                              
                                                                                                                                        
         run;quit;                                                                                                                      
      '));                                                                                                                              
                                                                                                                                        
       %put &=zroOne;                                                                                                                   
                                                                                                                                        
                                                                                                                                        
                                                                                                                                        
    *************************************                                                                                               
    3. Macro string (0,0,0,0,1,1,1,1,1,1)                                                                                               
       A lot of Klingon                                                                                                                 
    *************************************                                                                                               
                                                                                                                                        
                                                                                                                                        
      %let Zro = 4;                                                                                                                     
      %let One = 6;                                                                                                                     
                                                                                                                                        
        %let zroOne=(%sysfunc(repeat(%str(0,),%eval(&Zro-1)))%sysfunc(repeat(%str(1,),%eval(&One-2))),1);                               
                                                                                                                                        
        %put &=zroOne;                                                                                                                  
                                                                                                                                        
                                                                                                                                        
