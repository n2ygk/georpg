# georpg
Just messing around for Lisa trying to solve
[this puzzle](https://www.geocaching.com/geocache/GC6Y1J1_get-with-the-program)

## IBM 1130 and RPG simulator
Get an [IBM1130](http://media.ibm1130.org/sim/ibm1130.zip) and
[RPG II simulator](http://media.ibm1130.org/sim/rpgpreview.zip) from
http://ibm1130.org/sim/downloads

Read the
[RPG II reference manual](https://publib.boulder.ibm.com/iseries/v5r1/ic2924/books/c0918180.pdf)

Build the simulator (ignore the errors).
```bash
make
```

Test RPG with the demo program:
```bash
ibm1130$ ./ibm1130 runrpg rpg

IBM 1130 simulator V3.8-0
runrpg> * this script file sets up the system so that
Unknown command
runrpg> * you can use the GUI to process jobs
Unknown command
runrpg> * The RPG 1132 printer drivers are slower than
Unknown command
runrpg> * the ones encountered previously; allow more time
Unknown command
runrpg> * between printer and card reader interrupts to avoid 
Unknown command
runrpg> * Print Check errors. The card reader has to be slowed
Unknown command
runrpg> * down otherwise it can starve the printer driver of CPU cycles.
Unknown command
runrpg> dep ctime 3000
Invalid argument
PRT: creating new file
Loaded DMS V2M12 cold start card

Wait, IAR: 0000002A (4c80 BSC  I  ,0028   )

Use the "tear" button to view the output
sim> ^C
ibm1130$ cat printer.txt 

PAGE   1

// JOB    1234

LOG DRIVE   CART SPEC   CART AVAIL  PHY DRIVE
  0000        1234        1234        0000

V2 M12   ACTUAL 16K  CONFIG 16K


PAGE   1

// JOB

LOG DRIVE   CART SPEC   CART AVAIL  PHY DRIVE
  0000        1234        1234        0000

V2 M12   ACTUAL 16K  CONFIG 16K

// RPG


PAGE   2
                                      V1-3  1130  RPG   RPGOBJ


   SEQ NO  PG LIN    SPECIFICATIONS COL 6 - 74                                            ERRORS


           01 010    H
    0001   01 020    FBALANCE IPE F      80            READ42
    0002   01 030    FFINCHRGEO   F     120     OF     PRINTER
    0003   02 010    IBALANCE AA  01
    0004   02 020    I                                        1   52BALFOR
    0005   03 010    C   01      BALFOR    COMP 6                    11  11
    0006   03 020    C   11      BALFOR    MULT 0.18      INTRST  52H
    0007   03 030    C  N11                MOVE 1.00      INTRST  52
    0008   04 010    OFINCHRGEH 1201
    0009   04 020    O       OR        OF
    0010   04 030    O                                   30 'BALANCE FINANCE CHARGE'
    0011   04 040    O        D  1     01
    0012   04 050    O                         BALFOR    15 '$  0.  '
    0013   04 060    O                         INTRST    30 '      $  0.  '


PAGE   3
                                    INDICATORS

IND   DISP      IND   DISP      IND   DISP      IND   DISP      IND   DISP      IND   DISP

MR    0150      00    0151      OF    0152      OV    0153      1P    0154      L0    0155
L1    0156      L2    0157      L3    0158      L4    0159      L5    015A      L6    015B
L7    015C      L8    015D      L9    015E      LR    015F      H1    0160      H2    0161
H3    0162      H4    0163      H5    0164      H6    0165      H7    0166      H8    0167
H9    0168      01    0169      11    016A


                                    FIELD NAMES

FIELD   DISP  L  T D    FIELD   DISP  L  T D    FIELD   DISP  L  T D    FIELD   DISP  L  T D

BALFOR  016B 005 N 2    INTRST  0171 005 N 2


                                          LITERALS

        LITERAL           LENGTH   TYPE   DISP            LITERAL           LENGTH   TYPE   DISP
6                            1       N    0177    0.18                         3       N    0179
1.00                         3       N    017D    BALANCE FINANCE CHARGE      22       A    0181
    .                        7       E    0198          $   .                 13       E    01A0



                    EXTENDED CALCULATION SPECIFICATION DIAGNOSTICS        SEQ. NO.      ERROR

                                                                            0006        NOTE  188


              DIAGNOSTIC MESSAGE EXPLANATIONS

  NOTE   188    C  RSLT FLD LNG COL 49-51 MAY NOT BE LARGE ENOUGH

                                    KEY ADDRESSES OF OBJECT PROGRAM

  NAME OF ROUTINE             HEX DISP                NAME OF ROUTINE             HEX DISP

    H + D LINES                 0370                    TOTAL LINES                 037E
    DETAIL CALCS                033C                    TOTAL CALCS                 0359
    CHAIN ROUT 1                02E6                    LOW FIELD                   02FC
    EXCPT LINES                 038C                    CLOSE FILES                 04A3
    FILE SEQ 1                  0200                    FILE SEQ 2                  028B

END OF COMPILATION

// XEQ                     X



        BALANCE FINANCE CHARGE



        BALANCE FINANCE CHARGE

        $100.40          18.07



        BALANCE FINANCE CHARGE

        $  2.00          11.00



        BALANCE FINANCE CHARGE

        $123.45          22.22
```

## Fix runrpg to take paramterized job name.

Fixed [runrpg](./runrpg) to use `%1` parameter for the RPG job basename.

## Convert the sample program image to text

Waste time screwing around with some OCR tools then just type it all.
Hopefully get the spacing right. Use the reference manual to get the
spacing right.

See [geocache.job](./geocache.job).

When run it hangs the 1130 simulator and locks up the TTY. Kill the process from elsewhere.
Looking at the printer.txt there are a few compiler errors it looks like.

```bash
ibm1130$ ./ibm1130 runrpg geocache

IBM 1130 simulator V3.8-0
runrpg> * this script file sets up the system so that
Unknown command
runrpg> * you can use the GUI to process jobs
Unknown command
runrpg> * The RPG 1132 printer drivers are slower than
Unknown command
runrpg> * the ones encountered previously; allow more time
Unknown command
runrpg> * between printer and card reader interrupts to avoid 
Unknown command
runrpg> * Print Check errors. The card reader has to be slowed
Unknown command
runrpg> * down otherwise it can starve the printer driver of CPU cycles.
Unknown command
runrpg> dep ctime 3000
Invalid argument
PRT: creating new file
Loaded DMS V2M12 cold start card
Terminated: 15
ibm1130$ 
```

```

PAGE   1

// JOB    1234

LOG DRIVE   CART SPEC   CART AVAIL  PHY DRIVE
  0000        1234        1234        0000

V2 M12   ACTUAL 16K  CONFIG 16K

PAGE   1

// JOB

LOG DRIVE   CART SPEC   CART AVAIL  PHY DRIVE
  0000        1234        1234        0000

V2 M12   ACTUAL 16K  CONFIG 16K

// RPG

PAGE   2
                                      V1-3  1130  RPG   QCY1J1


   SEQ NO  PG LIN    SPECIFICATIONS COL 6 - 74                                            ERRORS


                     H 64                                                                 QCY1J1
    0001             FQCY1J1  UP  F      64            DISK
    ******           E                     LOOK       20  1
                                                                                        NOTE  030
                                                                                        NOTE  033
                                                                                        NOTE  034
                                                                                        NOTE  035
                                                                                        NOTE  038
    ******           E                     CACHER     51  20
                                                                                        NOTE  030
                                                                                        NOTE  033
                                                                                        NOTE  034
                                                                                        NOTE  035
                                                                                        NOTE  038
    ******           E                     CHARAC     62  1  A
                                                                                        NOTE  030
                                                                                        NOTE  033
                                                                                        NOTE  034
                                                                                        NOTE  035
                                                                                        NOTE  038
    0002             IQCY1J1  NS  01
    0003             I                                    P   1   43LATSTA
    0004             I                                    P   5   83LONSTA
    ******           I            DS
                                                                                        NOTE  131
    0005             I                                        1   73NWORK7
    0006             I                                        3   73NWORK5
    ******           I            DS
                                                                                        NOTE  131
    0007             I                                        1   50CHKSUM
    0008             I                                        1   10CHK1
    0009             I                                        2   20CHK2
    0010             I                                        3   30CHK3
    0011             I                                        4   40CHK4
    0012             I                                        5   50CHK5
    0013             I                                        2   30CHK23
    0014             I                                        4   50CHK45
                     C**************************************************************************
    0015             C                     Z-ADD*ZERO      FACTOR  50
                                                                                        NOTE  083
                                                                                        NOTE  094
                                                                                        NOTE  094
                                                                                        NOTE  089

```

## Still TODO:
Figure out how to get the three input/output files onto the disk:
- [LOOK](./look.txt)
- [CACHERS](./cachers.txt)
- [CHARAC](./charac.txt)

This looks like I just need to learn some JCL to read the file(s).
