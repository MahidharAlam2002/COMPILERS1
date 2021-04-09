# MINI ASSIGNMENT 1 : COMPILERS 1 : CS19BTECH11046

## VARIOUS OPTIONS IN GCC COMPILER :

The preprocessing, compilation, assembly, linking can be done by invoking GCC compiler. Lets go through a few options of GCC:
### OPTIONS IN GCC:
Overall options provided by the GCC helps us to stop these processes at any intermediate stage we want. -S, -o file, -c, -x language, -v, -E, -###  are a few examples for overall options. 
- -S helps in stopping the process after compilation proper and will not allow to assemble. Thus, the output for the non-assembler input file will be an assembler code file with the suffix .s but the name being the same (i.e. if input is file_name.c, the output file is file_name.s). If the given input file doesn’t require compilation then it is ignored.
- -v, prints the commands that are executed to do the stages in the compilation and prints the version of the compiler driver program, preprocessor, compiler proper.
- -c,  Stops gcc from doing linking stage but allows to compile or assemble the input files given. The output is a object file for each particular input or source file given. The name of the outfile is same as that of the input file except the suffix is .o.

### C LANGUAGE OPTIONS:
-ansi, -ffreestanding, -fopenacc, -flax-vector-conversions, -fgimple, -fopenmp are a few examples that come under C language options of gcc.
- -fopenmp, helps us in enabling the handling of OpenMP’s SIMD directives with #pragma omp in c and in Fortran, !$omp. 
- -fopenmp-simd, every OpenMP directives is ignored in this case but only enables the handling of #pragma omp in C and !$omp in Fortran.
- -fgimple, helps in enabling the function definitions marked with __GIMPLE.

### C++ LANGUAGE OPTIONS:
-Wnamespaces, -frepo, -Wtemplates, Wnarrowing, -Wregister, -Wnoexcept, -Wno-except-type, -fcheck-new, -Wabi-tag, -Wclass-mmemacess etc come under this category of GCC options.
- -Wnoexcept, warns the user when a noexcept-expression evaluates to false due to function that doesn’t have non-throwing exception specification but is known by the compiler to never throw an exception.

### OPTIMIZATION OPTIONS:
-O, -O0, -O1, -O2, -O3, -Os, -Ofast, -Og and many other come under the optimization options of GCC.
- -O0, here no optimization is done and the given source code is compiled in the default way.
- -O1 and -O are the same things. Here, the compiler reduces execution time of the code, size of the code but the optimizing compilation takes more amount of time and memory for large function.
- -O2, here the level of optimization is even more increased. The compiler takes lesser amount of time for execution of the code compared to O1 but takes the more amount of time, memory compared to -O1. Optimizations that doesn’t ned space-speed tradeoffs are used.
- -O3, does further more optimizations. These optimizations are generally not encouraged. It helps in fastening the resultant executable and in result also increases its size. It also does the all the things that -O2 can do.
- -Os, helps in the optimization of size of the code and also does all the optimizations of -O2 that will not result in increase of the size of the code.
- -Ofast, can do all optimizations that -O3 can do and in addition also does optimizations that are in valid for each and every standard-complaint programs. 
(There are a huge number of many other options as well in GCC, so only a good number of options are discussed here). 

### OPTIONS IN CLANG:
Stage selection options:
- -E, does the running of preprocessor stage. 
- -fsyntax-only, does the running of preprocessor, parser, type checking stages.
- -S, runs all the above mentioned ones and also the LLVM generated and optimizing sages finally produces the assembly - file as the output file.
- -c, runs all above things and additionally does the assembler stage and the final output will be a file with the same name that of source code but with ‘o suffix.

### LANGUAGE SELECTION AND MODE OPERATION:
-x <language>, -std=<standard>, -stdlib=<library>, -rtlib=<library>, -ansi, -ObjC, -ObjC++, -trigraphs, -ffreestanding, -fms-extensions, -fmsc-version, -fborland-extensions are a few which fall under this category of LLVM options.
### CODE GENERATION OPTIONS:
- -O0, it does no optimization, fastest compilation occurs here and the most debuggable code is generated in this case.
- -O1, optimization level is between -O0, -O2.
- -O2, level of optimization is moderate. Most of the optimizations are enabled in this case. 
- -O3, does all that of -O2 but also does a few optimizations that take more time to perform and also generates a longer code, i.e., size of code is increased in this case.
- -Os, does everything that -O2 does except that result in increase in size of the code.
- -Oz, does all that -Os does but reduces the size of code even more.

(There are a huge number of other options in clang/llvm, so only a good number of options are discussed here).

## FRONTENDS SUPPORTED BY GCC, LLVM:
(For now, currently) GCC supports frontends for C, C++, Fortran, Go, Objective C, Ada, D.
(For now, currently) LLVM supports frontends for Swift, C, C++, Fortran, Julia, Ada, D, Objective-C, Delphi, Rust. 
But, in the futures there are plans going on to widespread the support of frontends to Mercury (functional language), GNU Pascal Compiler (GPC), GHDL, GCC Unified Parallel C (GCC UPC) etc languages as well by GCC.


## REPORT AFTER THE FOLLOWING C CODE RUN ON OPTIMIZATION OPTIONS IN GCC:
```sh
#include<stdio.h>
#include<stdlib.h>
#include<pthread.h>

void *digi(void*n);

int main(){
	pthread_t p;
	int n=100;
	//printf("Enter a number : ");
	//scanf("%d",&n);
	pthread_create(&p,NULL,digi,&n);
	pthread_join(p,NULL);
	printf("The factors of %d are; ",n);
	for(int i=1;i<=n;i++){
		if(n%i==0){
			printf("%d ",i);
		}
	}
	return 0;
}

void *digi(void*n){
	int i=0;
	int m=*(int*)n;
	while(m!=0){
		m=(m)/10;
		i++;
	}
	printf("number of digits= %d\n",i);
	pthread_exit(NULL);
}

// to compile: gcc filename.c -lpthread
// to run: ./a.out
```

(The above is a simple C language souce code which creates a child thread which prints the factors of 100 whereas the main thread prints number of digits in it. (Save the file as h.c in home directory)).
clarealy it is a very small text(program) so changes in the size of code may not be observed due to max optimization achieved at the early stages itself, may be at -O1 or -O2, so changes in size, time may not be noticed here).

- Go to terminal and type the 1st line of below report and then the next command time ./a.out, it prints the output of the above code and then prints the real time, user time, sys time during the entire process.
- Next, type 'size ./a.out' it prints the a table kind of data as shown in each case.
- 
The below is result of -O0 optimization in gcc.  (No much optimization occurs, a default one actually).
```sh
gcc -Wall -O0 h.c -lpthread
time ./a.out
number of digits= 3
The factors of 100 are; 1 2 4 5 10 20 25 50 100 
real	0m0.004s
user	0m0.001s
sys	0m0.004s
size ./a.out
   text	   	 data	  bss	dec	    hex	filename
   2361	    648	      8	   3017	    bc9	./a.out
```
The below is result of -O1 optimization in gcc. (The effect of optimization on size of code and times can be seen clearly in each of the below cases).
```sh
gcc -Wall -O1 h.c -lpthread
time ./a.out
number of digits= 3
The factors of 100 are; 1 2 4 5 10 20 25 50 100 
real	0m0.003s
user	0m0.001s
sys	0m0.003s
size ./a.out
   text	    data	  bss	   dec	    hex	    filename
   2403	    648	      8	       3059	    bf3 	./a.out
```
The below is result of -O2 optimization in gcc.(The time taken became much lower but size remained almost same).
```sh
gcc -Wall -O2 h.c -lpthread
time ./a.out
number of digits= 3
The factors of 100 are; 1 2 4 5 10 20 25 50 100 
real	0m0.002s
user	0m0.000s
sys	0m0.003s
size ./a.out
   text	            data	    bss	  dec	    hex	filename
   2403	    648	      8	          3059	    bf3	         ./a.out
   ```
The below is result of -O3 optimization in gcc.(Time taken reduced again)
```sh
gcc -Wall -O3 h.c -lpthread
time ./a.out
number of digits= 3
The factors of 100 are; 1 2 4 5 10 20 25 50 100 
real	0m0.001s
user	0m0.000s
sys	0m0.001s
size ./a.out
   text	            data	    bss        dec	    hex	filename
   2403	    648	      8	        3059	    bf3	          ./a.out
```
The below is result of -Os optimization in gcc  (Very clearly we can observe that the size of code reduced a lot)
```sh
gcc -Wall -Os h.c -lpthread
time ./a.out
number of digits= 3
The factors of 100 are; 1 2 4 5 10 20 25 50 100 
real	0m0.004s
user	0m0.004s
sys	0m0.001s
size ./a.out
   text	            data	    bss          dec	    hex	filename
   2355	    648	      8	         3011	    bc3	./a.out
```
The below is result of -Ofast optimization in gcc.
```sh
gcc -Wall -Ofast h.c -lpthread
time ./a.out
number of digits= 3
The factors of 100 are; 1 2 4 5 10 20 25 50 100 
real	0m0.004s
user	0m0.004s
sys	0m0.000s
size ./a.out
   text	            data	    bss        dec	    hex	filename
   2491	    656	      8	        3155	    c53	./a.out
```   
Overall result : The time reduced as the higher optimizations are used and the size reduced a lot when -Os is used.


REPORT AFTER THE PREVIOUS C CODE RUN ON OPTIMIZATION OPTIONS IN CLANG/LLVM:
(The same above code pasted code is to be used in these cases as well). Clarealy it is a very small text(program) so changes in the size of code may not be observed due to max optimization achieved at the early stages itself, may be at -O1 or -O2, so changes in size, time may not be noticed here).

The below is result of -O0 optimization in CLANG/LLVM. (No much optimization occurs).
```sh
clang -Wall -O0 h.c -lpthread
time ./a.out
number of digits= 3
The factors of 100 are; 1 2 4 5 10 20 25 50 100 
real	0m0.004s
user	0m0.000s
sys	0m0.004s
size ./a.out
   text	    data	    bss	  dec	    hex	filename
   1785	    584	      8	        2377	    949	./a.out
```

The below is result of -O1 optimization in CLANG/LLVM.   (Time reduced and size as well).
```sh
clang -Wall -O1 h.c -lpthread
time ./a.out
number of digits= 3
The factors of 100 are; 1 2 4 5 10 20 25 50 100 
real	0m0.004s
user	0m0.000s
sys	0m0.003s
size ./a.out
   text	    data	    bss    dec	    hex	filename
   1681	    584	      8	   2273	    8e1	./a.out
```
The below is result of -O2 optimization in CLANG/LLVM.      (Time reduced but not much size).
```sh
clang -Wall -O2 h.c -lpthread
time ./a.out
number of digits= 3
The factors of 100 are; 1 2 4 5 10 20 25 50 100 
real	0m0.003s
user	0m0.000s
sys	0m0.001s
size ./a.out
   text	            data	    bss	    dec	    hex	filename
   1681	    584	      8	           2273	    8e1	./a.out
```
The below is result of -O3 optimization in CLANG/LLVM.  (Time reduced).
```sh
clang -Wall -O3 h.c -lpthread
time ./a.out
number of digits= 3
The factors of 100 are; 1 2 4 5 10 20 25 50 100 
real	0m0.001s
user	0m0.000s
sys	0m0.000s
size ./a.out
   text	   	data	   	 bss	    dec	    hex	filename
   1681	    584	      8	   2273	    8e1	./a.out
```
The below is result of -Os optimization in CLANG/LLVM. (The size of code is reduced very much considerably than the default situation).
```sh
clang -Wall -Os h.c -lpthread
time ./a.out
number of digits= 3
The factors of 100 are; 1 2 4 5 10 20 25 50 100 
real	0m0.004s
user	0m0.004s
sys	0m0.000s
size ./a.out
   text	   	data	    	bss	    dec	    hex	filename
   1673	    584	      8	   2265	    8d9	./a.out
```
The below is result of -Oz optimization in CLANG/LLVM.  (Size reduced again, which is clearly stated in the definition of the -Oz).
```sh
clang -Wall -Oz h.c -lpthread
time ./a.out
number of digits= 3
The factors of 100 are; 1 2 4 5 10 20 25 50 100 
real	0m0.004s
user	0m0.003s
sys	0m0.001s
size ./a.out
   text	   	data	    	  bss	      dec	    hex	filename
   1657	    584	      8	     2249	    8c9	./a.out
```
Overall result: Time is optimized as the level of optimization is increased and effect of -Os, -Oz is clearly seed on the size of code).


## GENERATING VARIOUS ARCHITECTURES FOR THE SAME ABOVE CODE USING GCC AND CLANG/LLVM COMPILER :
Type the below command in the terminal:
```sh
gcc h.c -S
```
Now type :
```sh
file h.s
```
In the terminal it ouputs like:
```sh
h.s: assembler source, ASCII text
```
Now go thee home directory and search for h.s file, we get that file in which the below is already printed:
```sh
	.file	"h.c"
	.text
	.section	.rodata
.LC0:
	.string	"The factors of %d are; "
.LC1:
	.string	"%d "
	.text
	.globl	main
	.type	main, @function
main:
.LFB6:
	.cfi_startproc
	endbr64
	pushq	%rbp
	.cfi_def_cfa_offset 16
	.cfi_offset 6, -16
	movq	%rsp, %rbp
	.cfi_def_cfa_register 6
	subq	$32, %rsp
	movq	%fs:40, %rax
	movq	%rax, -8(%rbp)
	xorl	%eax, %eax
	movl	$100, -24(%rbp)
	leaq	-24(%rbp), %rdx
	leaq	-16(%rbp), %rax
	movq	%rdx, %rcx
	leaq	digi(%rip), %rdx
	movl	$0, %esi
	movq	%rax, %rdi
	call	pthread_create@PLT
	movq	-16(%rbp), %rax
	movl	$0, %esi
	movq	%rax, %rdi
	call	pthread_join@PLT
	movl	-24(%rbp), %eax
	movl	%eax, %esi
	leaq	.LC0(%rip), %rdi
	movl	$0, %eax
	call	printf@PLT
	movl	$1, -20(%rbp)
	jmp	.L2
.L4:
	movl	-24(%rbp), %eax
	cltd
	idivl	-20(%rbp)
	movl	%edx, %eax
	testl	%eax, %eax
	jne	.L3
	movl	-20(%rbp), %eax
	movl	%eax, %esi
	leaq	.LC1(%rip), %rdi
	movl	$0, %eax
	call	printf@PLT
.L3:
	addl	$1, -20(%rbp)
.L2:
	movl	-24(%rbp), %eax
	cmpl	%eax, -20(%rbp)
	jle	.L4
	movl	$0, %eax
	movq	-8(%rbp), %rcx
	xorq	%fs:40, %rcx
	je	.L6
	call	__stack_chk_fail@PLT
.L6:
	leave
	.cfi_def_cfa 7, 8
	ret
	.cfi_endproc
.LFE6:
	.size	main, .-main
	.section	.rodata
.LC2:
	.string	"number of digits= %d\n"
	.text
	.globl	digi
	.type	digi, @function
digi:
.LFB7:
	.cfi_startproc
	endbr64
	pushq	%rbp
	.cfi_def_cfa_offset 16
	.cfi_offset 6, -16
	movq	%rsp, %rbp
	.cfi_def_cfa_register 6
	subq	$32, %rsp
	movq	%rdi, -24(%rbp)
	movl	$0, -8(%rbp)
	movq	-24(%rbp), %rax
	movl	(%rax), %eax
	movl	%eax, -4(%rbp)
	jmp	.L8
.L9:
	movl	-4(%rbp), %eax
	movslq	%eax, %rdx
	imulq	$1717986919, %rdx, %rdx
	shrq	$32, %rdx
	sarl	$2, %edx
	sarl	$31, %eax
	subl	%eax, %edx
	movl	%edx, %eax
	movl	%eax, -4(%rbp)
	addl	$1, -8(%rbp)
.L8:
	cmpl	$0, -4(%rbp)
	jne	.L9
	movl	-8(%rbp), %eax
	movl	%eax, %esi
	leaq	.LC2(%rip), %rdi
	movl	$0, %eax
	call	printf@PLT
	movl	$0, %edi
	call	pthread_exit@PLT
	.cfi_endproc
.LFE7:
	.size	digi, .-digi
	.ident	"GCC: (Ubuntu 9.3.0-17ubuntu1~20.04) 9.3.0"
	.section	.note.GNU-stack,"",@progbits
	.section	.note.gnu.property,"a"
	.align 8
	.long	 1f - 0f
	.long	 4f - 1f
	.long	 5
0:
	.string	 "GNU"
1:
	.align 8
	.long	 0xc0000002
	.long	 3f - 2f
2:
	.long	 0x3
3:
	.align 8
4:
```
In the same way using the clang compiler we can produce the assembler code with below command:
```sh
clang h.c -S
```
But the code may vary, we get following assembler code for it:
```sh
	.text
	.file	"h.c"
	.globl	main                    # -- Begin function main
	.p2align	4, 0x90
	.type	main,@function
main:                                   # @main
	.cfi_startproc
# %bb.0:
	pushq	%rbp
	.cfi_def_cfa_offset 16
	.cfi_offset %rbp, -16
	movq	%rsp, %rbp
	.cfi_def_cfa_register %rbp
	subq	$32, %rsp
	xorl	%eax, %eax
	movl	%eax, %esi
	movl	$0, -4(%rbp)
	movl	$100, -20(%rbp)
	leaq	-20(%rbp), %rcx
	leaq	-16(%rbp), %rdi
	movabsq	$digi, %rdx
	callq	pthread_create
	xorl	%r8d, %r8d
	movl	%r8d, %esi
	movq	-16(%rbp), %rdi
	movl	%eax, -28(%rbp)         # 4-byte Spill
	callq	pthread_join
	movl	-20(%rbp), %esi
	movabsq	$.L.str, %rdi
	movl	%eax, -32(%rbp)         # 4-byte Spill
	movb	$0, %al
	callq	printf
	movl	$1, -24(%rbp)
.LBB0_1:                                # =>This Inner Loop Header: Depth=1
	movl	-24(%rbp), %eax
	cmpl	-20(%rbp), %eax
	jg	.LBB0_6
# %bb.2:                                #   in Loop: Header=BB0_1 Depth=1
	movl	-20(%rbp), %eax
	cltd
	idivl	-24(%rbp)
	cmpl	$0, %edx
	jne	.LBB0_4
# %bb.3:                                #   in Loop: Header=BB0_1 Depth=1
	movl	-24(%rbp), %esi
	movabsq	$.L.str.1, %rdi
	movb	$0, %al
	callq	printf
.LBB0_4:                                #   in Loop: Header=BB0_1 Depth=1
	jmp	.LBB0_5
.LBB0_5:                                #   in Loop: Header=BB0_1 Depth=1
	movl	-24(%rbp), %eax
	addl	$1, %eax
	movl	%eax, -24(%rbp)
	jmp	.LBB0_1
.LBB0_6:
	xorl	%eax, %eax
	addq	$32, %rsp
	popq	%rbp
	.cfi_def_cfa %rsp, 8
	retq
.Lfunc_end0:
	.size	main, .Lfunc_end0-main
	.cfi_endproc
                                        # -- End function
	.globl	digi                    # -- Begin function digi
	.p2align	4, 0x90
	.type	digi,@function
digi:                                   # @digi
	.cfi_startproc
# %bb.0:
	pushq	%rbp
	.cfi_def_cfa_offset 16
	.cfi_offset %rbp, -16
	movq	%rsp, %rbp
	.cfi_def_cfa_register %rbp
	subq	$32, %rsp
	movq	%rdi, -8(%rbp)
	movl	$0, -12(%rbp)
	movq	-8(%rbp), %rax
	movl	(%rax), %ecx
	movl	%ecx, -16(%rbp)
.LBB1_1:                                # =>This Inner Loop Header: Depth=1
	cmpl	$0, -16(%rbp)
	je	.LBB1_3
# %bb.2:                                #   in Loop: Header=BB1_1 Depth=1
	movl	-16(%rbp), %eax
	cltd
	movl	$10, %ecx
	idivl	%ecx
	movl	%eax, -16(%rbp)
	movl	-12(%rbp), %eax
	addl	$1, %eax
	movl	%eax, -12(%rbp)
	jmp	.LBB1_1
.LBB1_3:
	movl	-12(%rbp), %esi
	movabsq	$.L.str.2, %rdi
	movb	$0, %al
	callq	printf
	xorl	%ecx, %ecx
	movl	%ecx, %edi
	movl	%eax, -20(%rbp)         # 4-byte Spill
	callq	pthread_exit
.Lfunc_end1:
	.size	digi, .Lfunc_end1-digi
	.cfi_endproc
                                        # -- End function
	.type	.L.str,@object          # @.str
	.section	.rodata.str1.1,"aMS",@progbits,1
.L.str:
	.asciz	"The factors of %d are; "
	.size	.L.str, 24

	.type	.L.str.1,@object        # @.str.1
.L.str.1:
	.asciz	"%d "
	.size	.L.str.1, 4

	.type	.L.str.2,@object        # @.str.2
.L.str.2:
	.asciz	"number of digits= %d\n"
	.size	.L.str.2, 22

	.ident	"clang version 10.0.0-4ubuntu1 "
	.section	".note.GNU-stack","",@progbits
	.addrsig
	.addrsig_sym pthread_create
	.addrsig_sym digi
	.addrsig_sym pthread_join
	.addrsig_sym printf
	.addrsig_sym pthread_exit
```
In the same way using 'gcc filename.c -c' and 'clang filename.c -c ' creates the files with .o suffixes but with the same middle name, that is like filename.o.

#                       /////      THE END     /////
