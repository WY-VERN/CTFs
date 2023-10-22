
# Cerial 01

we are given this file : cerial01: ELF 32-bit
bo the thig i had in mind was to run strings first .. couldn't find much ofc..
next i run in ghidra the file through GHidra , going to the main func we find some code 


the most interesting var that cought my eyes was: 
```python
  local_108c = "I&_9a%mx_tRmE4D3DmYw_9fbo6rd_aFcRbE,D.D>Y[!]!\'!q"
```

as the code will be generateed from this 
so as we can see in the code we need first to make this condition : 
      
```python
 iVar1 = memcmp(&DAT_00012039,local_1014,0xe);
if (iVar1 == 0){...}
```
and i just couldn't find a way to make it maybe there's a buffer overflow somewhere or something idk 
what i did was ignoring this check code and go to the part where the code is reassmbled 
measning this :
```python
for (; *local_108c != '\0'; local_108c = local_108c + 2) {
  *local_1088 = *local_108c;
  local_1088 = local_1088 + 1;
}
```

and execute it alone .
as it was easy it just takes a char in local_108c  then moved by 2 characters and takes the new character , that easy 
so here's the code solver in python :
```python
f="I&_9a%mx_tRmE4D3DmYw_9fbo6rd_aFcRbE,D.D>Y[!]!'!q"
g=[]
while f!="":
    g.append(f[0])
    f=f[2:]
    
print("".join(g))
```

after doing this you get the text: I_am_REDDY_for_FREDDY!!!
wrap in in flag{} to get the flag to submit as: flag{I_am_REDDY_for_FREDDY!!!}

and that was it 
