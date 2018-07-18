# ASCII Schematics

### Structure
```
|module|
  |submodule|
  |submodule|
```

### IDs
```
|1:module|
  |2:submodule|
  |3:submodule|
```

### Multipliers
```
|module|    just 1 
|module|x7  exact 7
|module||   some..
|module||*  0, 1 or many
|module||+  1 or many
```

### Relations

#### B/w 2 modules "in place"
```
|module1|
-[name]-    in both directions b/w 1 & 2
|module2|


|module1|
-[name]->   to 2 only
|module2|


|module1|
<-[name]-   to 1 only
|module2|
```

#### B/w modules as reference
```
|module1|
...
|module10|
...
|moduleX|-10 
         -1
or
|moduleX|-10 |-1  moduleX related to 1 & 10
```

### WIP
```
0,1>|ID:module|>2,3
   in          out
```
