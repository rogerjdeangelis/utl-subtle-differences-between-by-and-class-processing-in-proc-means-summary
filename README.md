# utl-subtle-differences-between-by-and-class-processing-in-proc-means-summary
Subtle differences between by and class processing in proc means summary  
    Subtle differences between by and class processing in proc means summary                                              
                                                                                                                          
    How to make 'class' and 'by' processing produce the same result.                                                      
                                                                                                                          
    Why you should use the 'missing option'.                                                                              
                                                                                                                          
    This not only makes 'by' and 'class' processing equivalent but                                                        
    provides 'missing' combinations'.                                                                                     
                                                                                                                          
    Problem: 'class' and 'by' processing do not produce the same results.                                                 
                                                                                                                          
      MEANS 'CLASS'                                                                                                       
        proc means noprint data=have nway;                                                                                
            class a b c;                                                                                                  
            var val;                                                                                                      
            output out=want(drop=_:) sum=wantclass;                                                                       
        run;                                                                                                              
                                                                                                                          
      MEANS 'by'                                                                                                          
        proc means noprint data=have nway ;                                                                               
            by a b c;                                                                                                     
            var val;                                                                                                      
            output out=want(drop=_:) sum=want;                                                                            
        run;                                                                                                              
                                                                                                                          
                                                                                                                          
    github                                                                                                                
    http://tinyurl.com/y2rcpdyy                                                                                           
    https://github.com/rogerjdeangelis/utl-subtle-differences-between-by-and-class-processing-in-proc-means-summary       
                                                                                                                          
    SAS Forum                                                                                                             
    https://communities.sas.com/t5/SAS-Programming/CLASS-vs-BY-in-PROC-MEANS/m-p/545427                                   
                                                                                                                          
    PaigeMiller                                                                                                           
    https://communities.sas.com/t5/user/viewprofilepage/user-id/10892                                                     
                                                                                                                          
    draycut                                                                                                               
    https://communities.sas.com/t5/user/viewprofilepage/user-id/31304                                                     
                                                                                                                          
                                                                                                                          
    And there is much more power when you use the CLASS command.                                                          
    First, you don't have to have the data sorted when you use the                                                        
    CLASS command. But when you use the CLASS command, you can also                                                       
    use the very powerful WAYS and TYPES commands in the same PROC call.                                                  
    So, for example, if you wanted the sum for each level of A; and the                                                   
    sum for each level of B, and so on, then this can't be done                                                           
     via the BY command; but this is easily done via:                                                                     
                                                                                                                          
                                                                                                                          
    *_                   _                                                                                                
    (_)_ __  _ __  _   _| |_                                                                                              
    | | '_ \| '_ \| | | | __|                                                                                             
    | | | | | |_) | |_| | |_                                                                                              
    |_|_| |_| .__/ \__,_|\__|                                                                                             
            |_|                                                                                                           
    ;                                                                                                                     
                                                                                                                          
    data have;                                                                                                            
                                                                                                                          
      length a $2;                                                                                                        
      do a=' ','A1','A2';                                                                                                 
         do b=.,1,2;                                                                                                      
            do c=1,2;                                                                                                     
               val=int(100*uniform(1234));                                                                                
               output;                                                                                                    
               val=int(100*uniform(1234));                                                                                
               output;                                                                                                    
            end;                                                                                                          
         end;                                                                                                             
      end;                                                                                                                
                                                                                                                          
    run;quit;                                                                                                             
                                                                                                                          
                                                                                                                          
    Up to 40 obs WORK.HAVE total obs=36                                                                                   
                                                                                                                          
    Obs    A     B    C    VAL                                                                                            
                                                                                                                          
      1          .    1     24                                                                                            
      2          .    1      8                                                                                            
                                                                                                                          
      3          .    2     38                                                                                            
      4          .    2      9                                                                                            
                                                                                                                          
      5          1    1     25                                                                                            
      6          1    1      8                                                                                            
      7          1    2      3                                                                                            
      8          1    2     10                                                                                            
      9          2    1     44                                                                                            
     10          2    1     14                                                                                            
     11          2    2      3                                                                                            
     12          2    2     45                                                                                            
     13    A1    .    1      8                                                                                            
     14    A1    .    1     90                                                                                            
     15    A1    .    2     96                                                                                            
     16    A1    .    2     73                                                                                            
     17    A1    1    1     40                                                                                            
     18    A1    1    1     37                                                                                            
     19    A1    1    2     32                                                                                            
     20    A1    1    2     51                                                                                            
     21    A1    2    1     28                                                                                            
     22    A1    2    1     35                                                                                            
     23    A1    2    2     25                                                                                            
     24    A1    2    2     43                                                                                            
     25    A2    .    1     12                                                                                            
     26    A2    .    1     71                                                                                            
     27    A2    .    2      0                                                                                            
     28    A2    .    2     51                                                                                            
     29    A2    1    1     90                                                                                            
     30    A2    1    1     23                                                                                            
     31    A2    1    2     79                                                                                            
     32    A2    1    2     14                                                                                            
     33    A2    2    1     11                                                                                            
     34    A2    2    1     53                                                                                            
     35    A2    2    2     64                                                                                            
     36    A2    2    2     77                                                                                            
                                                                                                                          
                                                                                                                          
    RULES                                                                                                                 
                                                                                                                          
     I want to sum val by A*B*c                                                                                           
                                                                                                                          
    *            _               _                                                                                        
      ___  _   _| |_ _ __  _   _| |_                                                                                      
     / _ \| | | | __| '_ \| | | | __|                                                                                     
    | (_) | |_| | |_| |_) | |_| | |_                                                                                      
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                                     
                    |_|                                                                                                   
    ;                                                                                                                     
                                                                                                                          
                                                                                                                          
    WANT                                                                                                                  
    ====                                                                                                                  
                                                                                                                          
    Up to 40 obs WORK.WANT total obs=18                                                                                   
                                                                                                                          
    Obs    A     B    C    WANT                                                                                           
                                                                                                                          
      1          .    1      32  ( 24+8)                                                                                  
                                                                                                                          
      2          .    2      47  (39+8)                                                                                   
                                                                                                                          
      3          1    1      33                                                                                           
      4          1    2      13                                                                                           
      5          2    1      58                                                                                           
      6          2    2      48                                                                                           
      7    A1    .    1      98                                                                                           
      8    A1    .    2     169                                                                                           
      9    A1    1    1      77                                                                                           
     10    A1    1    2      83                                                                                           
     11    A1    2    1      63                                                                                           
     12    A1    2    2      68                                                                                           
     13    A2    .    1      83                                                                                           
     14    A2    .    2      51                                                                                           
     15    A2    1    1     113                                                                                           
     16    A2    1    2      93                                                                                           
     17    A2    2    1      64                                                                                           
     18    A2    2    2     141                                                                                           
                                                                                                                          
                                                                                                                          
    ==========================                                                                                            
    HOWEVER I AM GETTING THIS.                                                                                            
    ==========================                                                                                            
                                                                                                                          
    proc means noprint data=have nway;                                                                                    
        class a b c;                                                                                                      
        var val;                                                                                                          
        output out=want(drop=_:) sum=wantclass;                                                                           
    run;                                                                                                                  
                                                                                                                          
    Up to 40 obs WORK.WANT total obs=8                                                                                    
                                                                                                                          
    Obs    A     B    C    WANTCLASS                                                                                      
                                                                                                                          
     1     A1    1    1        77                                                                                         
     2     A1    1    2        83                                                                                         
     3     A1    2    1        63                                                                                         
     4     A1    2    2        68                                                                                         
     5     A2    1    1       113                                                                                         
     6     A2    1    2        93                                                                                         
     7     A2    2    1        64                                                                                         
     8     A2    2    2       141                                                                                         
                                                                                                                          
    Missing Values are not computed.                                                                                      
                                                                                                                          
    Obs    A     B    C    WANT                                                                                           
                                                                                                                          
      1          .    1      32  ( 24+8)                                                                                  
                                                                                                                          
      2          .    2      47  (39+8)                                                                                   
                                                                                                                          
    *          _       _   _                                                                                              
     ___  ___ | |_   _| |_(_) ___  _ __                                                                                   
    / __|/ _ \| | | | | __| |/ _ \| '_ \                                                                                  
    \__ \ (_) | | |_| | |_| | (_) | | | |                                                                                 
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|                                                                                 
                                                                                                                          
    ;                                                                                                                     
                                                                                                                          
    Add missing optiion to means processing;                                                                              
                                                                                                                          
    These two 'proc means' yeild the required result.                                                                     
                                                                                                                          
                                      *******;                                                                            
    proc means noprint data=have nway MISSING;                                                                            
        class a b c;                  *******;                                                                            
        var val;                                                                                                          
        output out=want(drop=_:) sum=wantclass;                                                                           
    run;                                                                                                                  
                                                                                                                          
    You do not need the missing oution with 'by' processing.                                                              
    But I think it is a good idea.                                                                                        
                                      *******;                                                                            
    proc means noprint data=have nway missing;                                                                            
        by a b c;                     *******;                                                                            
        var val;                                                                                                          
        output out=want(drop=_:) sum=want;                                                                                
    run;                                                                                                                  
