




                                  README FIRST
        
        
        FILE 1 -- THIS INTRODUCTION
        
        This  is  the  long-awaited  Software Tools "Toys" tape where we
        bring you some of the major pieces of software  that  have  been
        written  since  the  first  "basic"  tape.  Hopefully, this will
        give everyone something to do while we  continue  to  smash  out
        standards  which  will  allow us to generate a new basic tape in
        the future. 
        
        This tape contains sources for format,  yacc,  lex,  ar,  RatFor
        and  LISP.   Format  is  the  Software  Tools formatter with tab
        stops added by the  Real  Time   Systems   Group   at   Lawrence
        Berkeley   Laboratory.     This  version   of   format  will  be
        necessary to read the documentation provided for yacc  and  lex.
        Yacc   and  Lex  are   Unix-like   language  development   tools
        developed  by RTSG. 

        Ar is an improved version of the Software Tools  archiver  which
        has  been taught to handle various flavors of archives including
        headers  with  character  counts,  headers  and  trailers,   and
        headers   and   trailers   with   characters   counts.   It  was
        contributed by Debbie Scherrer of Carousel Microtools. 

        The RatFor on the tape is the "almost"  standard  version  which
        narrowly  escaped  being blessed as our first standard language.
        It was contributed by Joe Sventek of the  Computer  Science  and
        Mathematics  (CSAM)  group at LBL.  All of the code on this tape
        should be compiled using this RatFor. 
        
        The LISP system on the  tape  is  a  new  development,  and  was
        contributed   by   Charlie  Dolan  and  Dave  Martin  of  Hughes
        Aircraft. 
        
        Also included on the  tape  are  test  programs  for  yacc   and
        lex.    There    is   also   an  archive  containing  5  support
        libraries which are needed by the yacc  and  lex  code  and  the
        test  programs.    The    following   sections  describe  the  7
        archives pertaining to format, yacc, lex, and ar. 
        
        
        FILE 2 -- RATDEF ARCHIVE
        
        The  Ratdef   archive   contains    RTSG's    standard    RatFor
        definition   file.    In   particular,   you   will   need   the
        definitions for P_, prints, printf, and fprintf in order to  use
        the   formatted   print  routines  (see the prilb archive in the
        Support Library archive). 








        
        
        FILE 3 -- FORMAT ARCHIVE
        
        The  Format  archive  consists  of  a   documentation   archive,
        an  include  file  archive,  and  a  source  code archive.  This
        formatter is  the  same as  the  formatter  distributed  on  the
        last  version  of the basic tape except that tab stops have been
        added  (.ta).  The documentation  for  Yacc  and  Lex  have  tab
        stops   in   them,   so   use   this  formatter  to  format  the
        documentation. 
        
        
        FILE 4 -- YACC ARCHIVE
        
        The yacc program  translates  a  yacc   compiler   specification
        into  an   executable   compiler.   It actually spawns to 3 main
        programs;  yaclr,  lrgen,  and  rc   (RatFor-compiler).    Yaclr
        extracts   the   user  supplied   RatFor code and translates the
        yacc   grammar   specification   into    an     lrgen    grammar
        specification.  Lrgen  translates  the  lrgen grammar  spec into
        LALR parse tables. The user-supplied RatFor code and  the  parse
        tables   are   then   compiled    and   linked   with  a support
        library   called   yyplb.   This    produces    an    executable
        compiler.  The  yacc  program  is  really just provided on  this
        tape as  an  example  of  how to create a program which will  do
        all  of  the   individual  tasks  required  to  compile  a  yacc
        compiler specification.  To  be  able  to  use  such  a  program
        you  must  be capable of doing spawns and you will probably have
        to  modifiy   it  to   correspond   to   your  RatFor   compiler
        conventions.  Otherwise  you  can  use yaclr and lrgen directly.
        The  following  3  sets   of    shell   commands    create    an
        executable    compiler   (assuming   your   RatFor  compiler  is
        called rc):
        
            1.  % yacc src/complr library
                
            2.  % yaclr -s src/complr.r src/complr | lrgen >> src/complr.r
                % rc src/complr.r yyplb library
                
            3.  % yaclr -s src/complr.r src/complr  > lrgram
                % lrgen < lrgram >> src/complr.r
                % rc src/complr.r yyplb library
        
        The main yacc archive  consists  of  a  yacc-tool   archive,   a
        yaclr  archive,   a  lrgen  archive,a lrglb archive, and a yyplb
        archive.  Lrglb is a set of support routines  for  lrgen,   i.e.
        lrgen   needs  to   link   with   lrglb   in  order  to compile.
        Yyplb is a set of 5 routines which all translated yacc  programs
        must  link  with.   Each  of  these  5  archives  consist  of  a








        documentation archive, an include file  archive,  and  a  RatFor
        source code archive. 

        [Editor's  note:   I  tried  building  yacc  and  found  routine
        "lastln" missing so I scrounged up RTSG's DEC version and  stuck
        it in the archive.]
        
        
        FILE 5 -- LEX ARCHIVE
        
        The  main  lex  archive  consists  of  a  yacc  lex  archive,  a
        skeleton lex  program  archive,  a  RatFor lex  archive,  and  a
        lexlb  archive.   Lex  is  written  in yacc. This requires  that
        you  implement  yacc before  implementing  lex.   However,   the
        3rd   archive   in  this section does include the translated lex
        program  (i.e.  the   output  from   yaclr   and    lrgen)    in
        RatFor.   So  if  you  have  problems  with  yacc,  you can just
        compile the RatFor  lex   program.   You   can   also  use   the
        RatFor  lex  program to test your yacc program (i.e. compare the
        output from using yaclr and lrgen on the yacc lex code). 
        
        The 2nd archive is a skeleton  program  which  lex   fills   out
        when  it   is   creating  a scanner.  Lex looks for the skeleton
        program, lexskel, in  a   lib   directory   using   searchpaths.
        RTSG   added  searchpaths  to  the  Software  Tools to implement
        a kind of UNIX Path variable. You  will  need  to   change   the
        string    declaration   for    the   skeleton   file  name  from
        "~/.%lib/lexskel" to  something  like  "/usr/lib/lexskel".  This
        declaration   is   on   line   1807  of src/lex. This is all you
        should need to change. 

        [Editor's note:  Again, I found some routines  missing  from  my
        system  which  may not have been on the basic tape.  They are in
        the "yacc.all" archive as file "missing".]
        
        
        FILE 6 -- SUPPORT LIBRARIES ARCHIVE
        
        The   support   libraries   archive    contains   documentation,
        include  files,  and  RatFor  sources  for  6 support libraries.
        These  libraries are  needed  for   yacc,   lex,  and  the  test
        programs.  They  are  NOT needed for ar or format. The 6 support
        libraries are:
        
            bslb - portable bit string routines
            tbllb - portable (rtsg-version) symbol table routines
            evalb - portable arithmetic expression evaluation routines
            quelb - portable queue manipulation routines
            memlb - portable dynamic memory routines
            vmemlb - VAX-dependent version of memlb (same interface)








            prilb - portable formatted print routines (fprintf,printf,prints)
        
        
        FILE 7 -- TUTORIALS ARCHIVE
        
        This archive contains a tutorial  for   lex   and   a   tutorial
        for   yacc.    Yacc    and   lex   were   developed  seperately.
        Unfortunately, they don't fit together exactly  like  UNIX  yacc
        and   lex.   One   of the  things  on  our  "wish  list"  is  to
        improve the interface between  yacc  and  lex.  Yacc  expects  a
        scanner   called    yylex,    like  UNIX.   Unfortunately,   Lex
        produces  a  scanner  routine  called lexscan. So basically  you
        need  to  supply  a  routine   called  yylex which calls the lex
        scanner, lexscan. 
        
        
        FILE 8 -- TEST ARCHIVE
        
        There  are  2  test  programs  for testing  yacc  and  lex.  The
        yacc  test  program  is   a   desk   calculator   tool,  dc.  It
        requires  2 support  libraries  evalb  and  tbllb.    Evalb   is
        an  expression  evaluation  library  and  tbllb  is  the  symbol
        table  library.  The  generated   dc   compiler   may   be   too
        large  for  your  computer  to  handle. You can make the dc tool
        smaller by deleting some of  the productions.   The   lex   test
        program   is  a  "ratfix"  tool,  i.e.  a  tool  which  converts
        old-style  RatFor  programs  to  the  new  RatFor language.   It
        basically  translates  all  old  definitions like LETD, NEWLINE,
        etc. to the new RatFor  constants,  'd',  '@n',  etc.  It   also
        changes    all   single-quoted  strings  to  double-quoted,  and
        changes  all  program   statements   to   DRIVER.   It   deletes
        initr4,   endr4  statements   and  inserts  DRETURN  statements.
        Again you can make it smaller if necessary by deleting  some  of
        the   rules.    Each   test  program   archive   consists  of  a
        documentation  archive,  an  include  file  archive,  a   source
        archive,  and  a  RatFor  source  archive.  The RatFor  versions
        will  allow  you  to  compare  your  lex and yacc output. 
        
        
        FILE 9 -- AR ARCHIVE
        
        This    archive    comes     from     Debbie     Scherrer     of
        Carousel  Microsystems.  It  is  basically  a  fixed  up version
        of the old archive. It handles character  counts,  headers,  and
        trailers.    The   archive    consists    of   a   documentation
        archive, an include file archive, and a RatFor source archive. 
        
        
        FILE 10 -- RATFOR ARCHIVE
        








        This is Joe Sventek's  latest  do-it-all  something-for-everyone
        RatFor  which  incorporates  all  the  bells  and  whistles  the
        standards  group  insisted  we  can't  live  without.    Several
        different   preprocessor   configurations   can   be  generated,
        especially in the area of string processing.  A second  pass  is
        now  available  for  reordering  statements according to ANSI-66
        specifications for those whose  FORTRAN  compilers  require  it.
        Again,  this  is  the  RatFor  you  should use when building the
        other tools on this tape. 
        
        
        FILE 11 -- LISP ARCHIVE
        
        And they said it couldn't be done!   A  reasonably  well-endowed
        LISP   interpreter   written   (almost)   entirely   in  RatFor.
        Originally  developed  for  an  HP-1000  minicomputer  (of   all
        things),  this LISP has been residing of late in the memory-rich
        VAX/VMS environment.  The basic overlaying strategy from the  HP
        has  been  retained,  however,  so  porting  it  back  down to a
        smaller machine  shouldn't  be  too  terrible.   If  you're  not
        running  on  a  VAX,  you'll  need  to write equivalents for the
        recursion-handling  routines   in   "rcrsv.mar".    Since   LISP
        requires  quite  a  few  primitives and library routines you may
        not have on your local  system,  we  have  included  our  entire
        runtime  library  as  archive  "rlib.ar"  in  the  LISP archive.
        Note:  Please don't  become  too  attached  to  this  particular
        dialect  of  LISP.   When COMMON LISP becomes available, we plan
        to rework this one to be as compatible as possible. 


        Have fun!  Send us YOUR toys for the next tape... 























                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            