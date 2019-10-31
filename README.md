# utl-copying-binary-files-from-one-directory-to-another-using-a-data-_null_
Copying binary files from one directory to another using a data _null_

    SAS Forum: Copying binary files from one directory to another using a data _null_                                                     
        
        
    Late arrivals

    I prefer to use operating system commads, but if you don't have an operating system you cam

    try

    I don't think dopen  supports the 'b'(binary) argument like fopen does.

    Also you can use 'recfm=n' or


    github
    https://tinyurl.com/y6qjceow
    https://github.com/rogerjdeangelis/utl-copying-binary-files-from-one-directory-to-another-using-a-data-_null_

    SAS Forum
    https://tinyurl.com/yyekhuxj
    https://communities.sas.com/t5/SAS-Programming/Move-multiple-files-in-SAS/m-p/593272

    Unix cp
    or
    windows
    robocopy
    xcopy

    github
    https://tinyurl.com/y4u776gf
    https://documentation.sas.com/?docsetId=lefunctionsref&docsetTarget=n10dz22b5ixohin1vwzilweetek0.htm&docsetVersion=9.4&locale=en

    Example 2: Copying a Binary File
    This example copies a binary file from one directory to another. Setting the
    MSGLEVEL= system option to I causes informational messages from FCOPY to be written to the log.
       /* Set MSGLEVEL to I to write messages from FCOPY to the log. */
    options msglevel=i;

    filename src 'raises.xlsx' recfm=n;
    filename dest 'raises-2012.xlsx' recfm=n;

       /* Create an example file to copy. */
    data _null_;
       file src;
       do i=1, 2105, 300312, 400501;
         put i:words256.;
       end;
    run;

    data _null_;
       length msg $ 384;
       rc=fcopy('src', 'dest');
       if rc=0 then
          put 'Copied SRC to DEST.';
       else do;
          msg=sysmsg();
          put rc= msg=;
       end;
    run;


                                                                                                                                      
    Problem;                                                                                                                              
                                                                                                                                          
        Copy                                                                                                                              
           d:/xls/one.xlsx                                                                                                                
           d:/xls/two.xlsx                                                                                                                
           d:/xls/tre.xlsx                                                                                                                
        To                                                                                                                                
           d:/xlsx/one.xlsx                                                                                                               
           d:/xlsx/two.xlsx                                                                                                               
           d:/xlsx/tre.xlsx                                                                                                               
                                                                                                                                          
    Note: It is better to use operating system commands that handle binary data ( robocopy xcopy)                                         
    I do understand that most of the EG users may not have an operting sysyem.                                                            
                                                                                                                                          
    github                                                                                                                                
    https://tinyurl.com/y6qjceow                                                                                                          
    https://github.com/rogerjdeangelis/utl-copying-binary-files-from-one-directory-to-another-using-a-data-_null_                         
                                                                                                                                          
    SAS Forum                                                                                                                             
    https://tinyurl.com/yyekhuxj                                                                                                          
    https://communities.sas.com/t5/SAS-Programming/Move-multiple-files-in-SAS/m-p/593272                                                  
                                                                                                                                          
    Macro on end and in github macro libraries (Bruno Mueller)                                                                            
                                                                                                                                          
    https://tinyurl.com/y3bsx3db                                                                                                          
    https://github.com/rogerjdeangelis/utl-macros-used-in-many-of-rogerjdeangelis-repositories/blob/master/binaryfilecopy.sas             
                                                                                                                                          
    macros ( substitutes double quotes for single quotes so I could use the macro with dosubl )                                           
    https://tinyurl.com/y9nfugth                                                                                                          
    https://github.com/rogerjdeangelis/utl-macros-used-in-many-of-rogerjdeangelis-repositories                                            
                                                                                                                                          
    *_                   _                                                                                                                
    (_)_ __  _ __  _   _| |_                                                                                                              
    | | '_ \| '_ \| | | | __|                                                                                                             
    | | | | | |_) | |_| | |_                                                                                                              
    |_|_| |_| .__/ \__,_|\__|                                                                                                             
            |_|                                                                                                                           
    ;                                                                                                                                     
                                                                                                                                          
    * create directories and files;                                                                                                       
                                                                                                                                          
    data _null_;                                                                                                                          
       rc=dcreate("xls","d:/");                                                                                                           
       rc=dcreate("xlsx","d:/");                                                                                                          
    run;quit;                                                                                                                             
                                                                                                                                          
    libname xla "d:/xls/one.xlsx";                                                                                                        
    libname xlb "d:/xls/two.xlsx";                                                                                                        
    libname xlc "d:/xls/tre.xlsx";                                                                                                        
                                                                                                                                          
    data xla.one xlb.two xlc.tre;                                                                                                         
       set sashelp.stocks( obs=30);                                                                                                       
       select ;                                                                                                                           
            when (mod(_n_,3)=0) output xla.one;                                                                                           
            when (mod(_n_,4)=0) output xlb.two;                                                                                           
            when (mod(_n_,5)=0) output xlc.tre;                                                                                           
            otherwise;                                                                                                                    
       end;                                                                                                                               
    run;quit;                                                                                                                             
                                                                                                                                          
    libname xla clear;                                                                                                                    
    libname xlb clear;                                                                                                                    
    libname xlc clear;                                                                                                                    
                                                                                                                                          
    d:/xls/one.xlsx                                                                                                                       
    d:/xls/two.xlsx                                                                                                                       
    d:/xls/tre.xlsx                                                                                                                       
                                                                                                                                          
    *            _               _                                                                                                        
      ___  _   _| |_ _ __  _   _| |_                                                                                                      
     / _ \| | | | __| '_ \| | | | __|                                                                                                     
    | (_) | |_| | |_| |_) | |_| | |_                                                                                                      
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                                                     
                    |_|                                                                                                                   
    ;                                                                                                                                     
                                                                                                                                          
    WORK.LOG total obs=3                                                                                                                  
                                                                                                                                          
      FILE    RC        STATUS                                                                                                            
                                                                                                                                          
      one      0    copy successful                                                                                                       
      two      0    copy successful                                                                                                       
      tre      0    copy successful                                                                                                       
                                                                                                                                          
                                                                                                                                          
    d:/xls/one.xlsx                                                                                                                       
    d:/xls/two.xlsx                                                                                                                       
    d:/xls/tre.xlsx                                                                                                                       
                                                                                                                                          
    *                                                                                                                                     
     _ __  _ __ ___   ___ ___  ___ ___                                                                                                    
    | '_ \| '__/ _ \ / __/ _ \/ __/ __|                                                                                                   
    | |_) | | | (_) | (_|  __/\__ \__ \                                                                                                   
    | .__/|_|  \___/ \___\___||___/___/                                                                                                   
    |_|                                                                                                                                   
    ;                                                                                                                                     
                                                                                                                                          
                                                                                                                                          
    data _null_;                                                                                                                          
                                                                                                                                          
      do file="one","two","tre";                                                                                                          
                                                                                                                                          
        call symputx("file",file);                                                                                                        
                                                                                                                                          
        rc=dosubl('                                                                                                                       
            filename _bcin "d:/xls/&file..xlsx";                                                                                          
            filename _bcout "d:/xlsx/&file..xlsx";                                                                                        
            %binaryFileCopy(                                                                                                              
              infile=_bcin                                                                                                                
             ,outfile=_bcout                                                                                                              
             ,chunkSize=16392                                                                                                             
         );');                                                                                                                            
      end;                                                                                                                                
                                                                                                                                          
      stop;                                                                                                                               
                                                                                                                                          
    run;quit;                                                                                                                             
                                                                                                                                          
    *                                                                                                                                     
     _ __ ___   __ _  ___ _ __ ___                                                                                                        
    | '_ ` _ \ / _` |/ __| '__/ _ \                                                                                                       
    | | | | | | (_| | (__| | | (_) |                                                                                                      
    |_| |_| |_|\__,_|\___|_|  \___/                                                                                                       
                                                                                                                                          
    ;                                                                                                                                     
                                                                                                                                          
    /**********************************************************************************************                                       
    Description                                                                                                                           
    -----------                                                                                                                           
    This macro will do a binary file copy from one fileref to another fileref                                                             
    The filerefs need to be assigned outside of the macro.                                                                                
    No special RECFM settings are necessary.                                                                                              
    The FILENAME statement can use special file-access-methods such as URL, FTP, WEBDAV                                                   
                                                                                                                                          
    The code makes use of the FOPEN, FREAD, FGET, etc functions to do the processing,                                                     
    as they support binary reading mode                                                                                                   
                                                                                                                                          
    Input Parameters                                                                                                                      
    ----------------                                                                                                                      
    infile     : optional, contains the source fileref                                                                                    
                 default = _BCIN                                                                                                          
                                                                                                                                          
    outfile    : optional, contains the target fileref                                                                                    
                 default = _BCOUT                                                                                                         
                                                                                                                                          
    returnName : optional, the return code macro variable name can be specified                                                           
                 here                                                                                                                     
                 default = _BCRC                                                                                                          
                                                                                                                                          
    chunkSize  : optional, specify the number of bytes to be processed in one operation                                                   
                 this will affect the time it takes to copy a file,                                                                       
                 smaller values mean longer process time                                                                                  
                 default = 8196                                                                                                           
                 max = 32767 (max length for var)                                                                                         
                                                                                                                                          
    Global Macro Variables                                                                                                                
    ----------------------                                                                                                                
    _BCRC      : 0 = successful, 4 = warning, 8 = error                                                                                   
                                                                                                                                          
    Example                                                                                                                               
    -------                                                                                                                               
                                                                                                                                          
    filename _bcin "C:\temp\someName.ext";                                                                                                
    filename _bcout webdav                                                                                                                
      "http://serverName:8080/SASContentServer/repository/default/sasdav/someName.ext"                                                    
      user="user"                                                                                                                         
      pass="pass"                                                                                                                         
    ;                                                                                                                                     
                                                                                                                                          
    %binaryFileCopy()                                                                                                                     
    %put NOTE: _bcrc=&_bcrc;                                                                                                              
                                                                                                                                          
    filename _bcin clear;                                                                                                                 
    filename _bcout clear;                                                                                                                
                                                                                                                                          
                                                                                                                                          
    History                                                                                                                               
    -------                                                                                                                               
    29Jan2013 Bruno Mueller, Initial Coding                                                                                               
    **********************************************************************************************/                                       
    %macro binaryFileCopy(                                                                                                                
      infile=_bcin                                                                                                                        
      , outfile=_bcout                                                                                                                    
      , returnName=_bcrc                                                                                                                  
      , chunkSize=16392                                                                                                                   
    );                                                                                                                                    
      %local                                                                                                                              
        startTime                                                                                                                         
        endTime                                                                                                                           
        diffTime                                                                                                                          
      ;                                                                                                                                   
                                                                                                                                          
      %let startTime = %sysfunc( datetime() );                                                                                            
                                                                                                                                          
      %if %sysevalf( &chunkSize > 32767 ) = 1 %then %do;                                                                                  
        %put NOTE: &sysMacroname chunksize > 32767, setting it to 32767;                                                                  
        %let chunksize = 32767;                                                                                                           
      %end;                                                                                                                               
                                                                                                                                          
      %put NOTE: &sysMacroname start %sysfunc( putn(&startTime, datetime19.));                                                            
      %put NOTE: &sysMAcroname infile=&infile %qsysfunc(pathname(&infile));                                                               
      %put NOTE: &sysMAcroname outfile=&outfile %qsysfunc(pathname(&outfile));                                                            
                                                                                                                                          
      *                                                                                                                                   
      * create global return var                                                                                                          
      *;                                                                                                                                  
      %if %symexist(&returnName) = 0 %then %do;                                                                                           
        %global &returnName;                                                                                                              
      %end;                                                                                                                               
                                                                                                                                          
      data _null_;                                                                                                                        
        retain cnt 0;                                                                                                                     
        length                                                                                                                            
          msg $ 1024                                                                                                                      
          rec $ &chunkSize                                                                                                                
          outfmt $ 32                                                                                                                     
        ;                                                                                                                                 
                                                                                                                                          
        *                                                                                                                                 
        * open input and output file with binary mode                                                                                     
        *;                                                                                                                                
        fid_in = fopen("&infile", "S", &chunkSize, "B");                                                                                  
                                                                                                                                          
        *                                                                                                                                 
        * check for unsuccessful open                                                                                                     
        *;                                                                                                                                
        if fid_in <= 0 then do;                                                                                                           
          msg = sysmsg();                                                                                                                 
          putlog "ERROR: &sysMacroname open failed for &infile";                                                                          
          putlog msg;                                                                                                                     
          call symputx("&returnName",8);                                                                                                  
          stop;                                                                                                                           
        end;                                                                                                                              
                                                                                                                                          
        fid_out = fopen("&outfile", "O", &chunkSize, "B");                                                                                
                                                                                                                                          
        *                                                                                                                                 
        * check for unsuccessful open                                                                                                     
        *;                                                                                                                                
        if fid_out <= 0 then do;                                                                                                          
          msg = sysmsg();                                                                                                                 
          putlog "ERROR: &sysMacroname open failed for &outfile";                                                                         
          putlog msg;                                                                                                                     
          call symputx("&returnName",8);                                                                                                  
          stop;                                                                                                                           
        end;                                                                                                                              
                                                                                                                                          
        *                                                                                                                                 
        * we will keep track on the number of bytes processed                                                                             
        *;                                                                                                                                
        bytesProcessed = 0;                                                                                                               
                                                                                                                                          
        *                                                                                                                                 
        * read loop on input file                                                                                                         
        *;                                                                                                                                
        do while( fread(fid_in) = 0 );                                                                                                    
          call missing(outfmt, rec);                                                                                                      
          rcGet = fget(fid_in, rec, &chunkSize);                                                                                          
                                                                                                                                          
          *                                                                                                                               
          * need this information for write processing                                                                                    
          *;                                                                                                                              
          fcolIn = fcol(fid_in);                                                                                                          
                                                                                                                                          
          *                                                                                                                               
          * need a format length to handle situations                                                                                     
          * where last chars in rec are blank                                                                                             
          * true: normal situation                                                                                                        
          * false: last chunk of data at end of file                                                                                      
          *;                                                                                                                              
          if (fColIn - &chunkSize) = 1 then do;                                                                                           
            fmtLength = &chunkSize;                                                                                                       
          end;                                                                                                                            
          else do;                                                                                                                        
            fmtLength = fColIn - 1;                                                                                                       
          end;                                                                                                                            
                                                                                                                                          
          *                                                                                                                               
          * prepare the output format                                                                                                     
          * and write rec                                                                                                                 
          *;                                                                                                                              
          outfmt = cats("$char", fmtLength, ".");                                                                                         
          rcPut = fput(fid_out, putc(rec, outfmt));                                                                                       
          rcWrite = fwrite(fid_out);                                                                                                      
                                                                                                                                          
          cnt=cnt+1;                                                                                                                      
          if mod(cnt,500) = 0 then putlog cnt=;                                                                                           
                                                                                                                                          
          *                                                                                                                               
          * keep track of bytes                                                                                                           
          *;                                                                                                                              
          bytesProcessed + fmtLength;                                                                                                     
                                                                                                                                          
          *                                                                                                                               
          * just in case                                                                                                                  
          *;                                                                                                                              
          maxRc = max(rcGet, rcPut, rcWrite);                                                                                             
          if maxRc > 0 then do;                                                                                                           
            putlog "ERROR: &sysMacroname checklog " rcGet= rcPut= rcWrite=;                                                               
            call symputx("&returnName", 8);                                                                                               
          end;                                                                                                                            
        end;                                                                                                                              
                                                                                                                                          
        putlog "NOTE: &sysMacroname processed " bytesProcessed "bytes";                                                                   
        rcInC = fclose(fid_in);                                                                                                           
        rcOutC = fclose(fid_out);                                                                                                         
        maxRc = max(rcInC, rcOutC);                                                                                                       
                                                                                                                                          
        if maxRc > 0 then do;                                                                                                             
          putlog "ERROR: &sysMacroname checklog " rcInC= rcOutC=;                                                                         
          call symputx("&returnName", 8);                                                                                                 
        end;                                                                                                                              
        else do;                                                                                                                          
          call symputx("&returnName", 0);                                                                                                 
        end;                                                                                                                              
      run;                                                                                                                                
                                                                                                                                          
      %let endTime = %sysfunc( datetime() );                                                                                              
      %put NOTE: &sysMacroname end %sysfunc( putn(&endTime, datetime19.));                                                                
      %let diffTime = %sysevalf( &endTime - &startTime );                                                                                 
      %put NOTE: &sysMacroname processtime %sysfunc( putn(&diffTime, tod12.3));                                                           
    %mend;                                                                                                                                
                                                                                                                                          
