##Contact information

Name : Prasun Anand

Email : prasunanand.bitsp@gmail.com

Github Username: prasunanand

**Why do you like Ruby, and why do you want to work on SciRuby?**


As a web developer, I was introduced to Ruby initially via Ruby on Rails and soon the beauty and the productivity of the language got me hooked on to it. In addition to the elegance of the language, a wonderful ecosystem and a very helpful community made it impossible for me to leave Ruby and this has been my go to language for all tasks, ranging from a simple script to complex web apps.

There is one thing that always bothered me though, people often associate ruby with only rails and usually do not know about other use cases of Ruby. Projects like SciRuby bring the best out of both worlds, increased productivity due to Ruby and also it opens up a whole new world of scientific tools to the Ruby community. I hope to see Ruby beyond just a language for web development, and for that I feel SciRuby is an excellent platform.

I have previously worked with Network X, for network analysis. I wanted to develop a web app which provides a GUI to study the network. So, I developed an app by integrating Networkx with Django.

However, if we had something similar like Networkx in Ruby, it would be amazing to just integrate it with rails. And Sciruby provides us that platform to create scientific libraries in Ruby.

**What do you like about science and why? What area do you like best?**

Science is all about how things work. It addresses a fundamental human need of curiosity. Human beings by nature are curious about figuring stuff out for themselves and once they have figured out the reason they want to develop on it creatively. Science provides this opportunity for reasoning and creativity to merge into one another. As a student there is perhaps no other field that lets me explore my creative and reasoning potential to an extent like science.

I would like to call myself a Bioinformatics enthusiast. I would love to develop tools that can help the Bioinformaticians around the world. I am interested in pursuing a Ph.D. in Computational Biology and this project would help me a lot in contributing to my expertise. This project  would be an amazing GSOC experience.

**Describe your experience with the following: Ruby, C, C++, other languages.**

C is the language through which I was introduced to Computer Programming in my first year of college. I prefer C for competitive coding.

I am a self-taught Computer Programmer. It started as a hobby when I wanted to develop some cool websites. I taught myself HTML, CSS, JS and PHP. I interned at Biotech Park, Lucknow, India, where I set-up a standalone BLAST server and developed a CRUD based application to study gene based biomarkers.

After that, I learnt Python, Django and AngularJS to develop the website where I was interning in the summers after my third year of college.

Ruby is very elegant. The coding style is what I like the most. While developing the new site for edu.biojs.net I had to learn Ruby to work with the existing codebase. Gradually, I learnt Ruby on Rails to develop websites.

While contributing to css-chassis project for Jquery Foundation, I dived deep into Javascript, learnt nodejs.

I have used Java to build parsers in my internship. Java is very robust and powerful in building enterprise software. I have a very little knowledge of Spring framework

**Describe your educational background (school, degree plan, major, past degrees, research area, publications, etc.).**

**Education:**

I am a fourth-year student at BITS Pilani KK Birla Goa Campus, Goa, India pursuing a dual degree in M.Sc. in Biological Sciences and B.E. in Chemical Engineering. I am inclined more towards Biological Sciences.

My research interest lies in Graph Theory, Neural Signal Processing. I have been integrating Networkx with Django to develop a web interface for study of Biological Networks as a part of my Study project. I have recently developed an interest in Neural Signal Processing. I would be doing a thesis on Neural Signal Processing in the next semester.

Currently, as a part of my study project in Chemical Engineering I am developing a software in Ruby to create  a Hierarchical Network for Multi-Level Inference. It mainly deals with socket programming to create a communication channel between process controllers and client machines.

Have you offered any pull requests for SciRuby or contributed in other ways? Please provide links, if possible. Past contributions are required, and must be in the form of code. Documentation contributions are also beneficial.
Work Experience:

**Open-source Contributions:**

  1. BioJavascript:



 - Created the growth curve for the stats page of BioJS. The website is
   hosted at stats.biojs.net. Worked with stockchart.js. Merged PR : [1]
 - Developed the new UI of edu page of BioJS. The website is hosted at
   edu.biojs.net. Worked with Jekyll, Bootstrap. Merged PR : [2]


  2.  Jquery Foundation:

Worked on the CSS-Chassis project. Added Semantic UI and Kendo-UI to the performance testing. Merged PRs : [3], [4]
        3.  Sciruby :
My idea is related to the issue #480 . I have also written a functional code that can be found here.
After the application submission , I will work on some issues on current NMatrix codebase that will enhance NMatrix functionalities which I can also use at the time of port.

**Gems Published**

Mitab Parser : A ruby parser for MITab file format.  https://rubygems.org/gems/mitab

The current code is working fine. I am being mentored by Pjotr Prins to improve the code; use of pure functional programming and introducing lazy parsing.

**What other commitments do you have this summer aside from GSoC? What obstacles do you foresee this summer as far as contributing the full forty hours per week during the GSoC period?**

None.

I do not think any obstacles would arise that would prevent me from committing forty hours per week in the summer period. If any unexpected obstacles do arise I would do my best to overcome them as I am quite excited to work in this project and it would take priority over everything else.

**Are you planning any fun vacations this summer?**

No

**How many classes are you taking this summer?**

0

**Do you have any other employment this summer?**

No

**Please talk a bit about any past GSoC projects in which you have participated. If you've done GSoC before, how could we reach your mentor(s)?**

None

**Please propose a project you would like to work on. Successful proposals will require advanced planning, communication with the project administrators and mentors, and likely a great deal of research on specific methods for achieving your project goals (e.g., what algorithms will you use? What frameworks?). A good place to start is the Ideas Page. You should also consider lurking on our IRC channel (#sciruby on FreeNode). Participation in listserv discussions is strongly recommended.**

# Project Proposal

## Title

Port NMatrix to JRuby.

## Abstract

NMatrix for MRI has become a fairly well-established project. However with JRuby+Truffle+Graal becoming very fast compared to MRI, a lot of ruby developers are switching to JRuby.
This project aims to port NMatrix to JRuby. JRuby compiles to byte code making it fast and also does heavy optimizations before and after generating byte code. Apache Commons Math will be used to build the core of NMatrix.

## Background

NMatrix is SciRuby's numerical matrix core, implementing dense matrices as well as two types of sparse (linked-list-based and Yale/CSR). It currently relies on ATLAS/CBLAS/CLAPACK and standard LAPACK for several of its linear algebra operations.

However NMatrix does not run on JRuby because of C-libraries, and as a result they're not usable on JRuby. The more of these libraries we have ports for, the less pain JRuby users suffer during migration.
JRuby is getting faster and faster and outperforms MRI 4-10x and is getting faster thanks to work by IBM and Oracle.


## Technical Description

**NMatrix core libraries in Java**

NMatrix for MRI uses ATLAS/CBLAS/CLAPACK libraries for implementing the core number crunching algorithms. For JAVA , we have an option of using COLT/Parallel COLT(used by mdarray) or Apache Commons, because they are the most mature and preferred libraries. We also have an option to use JBLAS. However it is not mature enough and it is not supported by 64-bit Windows machine. This wiki page tells why?

Each of these libraries have certain advantages and downsides.

**COLT/Parallel Colt:** COLT/Parallel Colt has less support.The homepage shows the latest version 0.10.1 was last published on 30 July 2013.

**Apache Commons Math:** Apache Commons Math provides better support. The homepage shows the latest version 15 was last published on 04 February 2016. However Apache Commons Math does not provide support for arbitrary dimensions.

The given article from 2013 on github compares different Java libraries for linear algebra which shows that Commons Math3.2 closely competes with Parallel Colt 0.9.4 in most of linear algebra functions.
I couldn’t find any recent article that compares Commons Math 3.6.1 with Parallel Colt 0.9.4.
So, I think that Apache Commons Math will be best suited to develop the core of NMatrix for JRuby.

**Dtypes(Boxing and Unboxing)**

NMatrix for MRI uses templates in C to implement mapping of dtypes. Generics in JAVA are analogous to templates in C. However, Generics are just syntactic sugar because of Type Erasure.
Sample code that I wrote to implement mapping of dtypes in JRuby.

I used the enumerated data types as in the C core of nmatrix. Currently , Generics has been loosely implement in my code. Also,in future we have an option of using singleton methods if we still get any issues implementing dtypes.

Commons Math Can Store Double Values, BigDecimal Values, Strings, Objects, Generic Objects, Complex Numbers. Generic Objects are implemented using the interface org.apache.commons.math.Field and will be helpful in implementing Float and Integer.

Common Maths: Matrices and vectors using non-real field elements can be used in Commons Math using FieldMatrix.

Functionalities

Apache Commons Math can be easily used to implement the following features for NMatrix for JRuby.
Dtypes
Stypes
Dense
Sparse
Basic Algebra Functions
Decomposition Algorithm
LU
Cholesky
QR
Eigen Decomposition
SVD

**Benchmarking**

I have implemented a basic sample of NMatrix for JRuby using Commons Math , and run basic algebraic functions namely addition, subtraction and matrix multiplication. I have compared them with NMatrix and NMatrix-ATLAS implemented on MRI and MDArray. The results of the benchmark are here:
https://github.com/prasunanand/jnmatrix/blob/master/benchmarking/results.txt



**Observations**

We can see that NMatrix for JRuby using Apache Commons Math is faster than NMatrix for MRI, for addition, subtraction and matrix multiplication.

NMatrix-ATLAS for MRI is amazingly fast for matrix multiplication.NMatrix-ATLAS for JRuby implemented using JBLAS wrappers has an almost similar benchmark time for matrix multiplication.
MDArray is the fastest for matrix addition while the slowest for matrix multiplication.
(Note: In the above benchmark results, I have not considered the warm up time for JVM.)

**Why not use MDArray?**

Mdarray is a multidimensional array implemented for JRuby. However, its syntax is not similar to nmatrix. The only possible way to run nmatrix on JRuby is to build a wrapper of nmatrix on Mdarray because COLT/ Parallel COLT which don’t provide any support lately.

So , in order to make nmatrix for JRuby (using mdarray-wrappers) fast we also need to optimize mdarray. I prefer writing NMatrix for JRuby by writing a wrapper Apache Commons Math.

NMatrix-ATLAS(using JBLAS) takes 0.3 seconds to multiply 1000*1000 matrix with a 1000*1000 matrix . MDArray being the slowest  takes 1.23 seconds and Apache Commons takes 0.97seconds.

However, If I use BlockMatrices, I can make multiplication even faster using Apache Commons . I haven't tested it but Apache Commons has mentioned it in their docs.

Also, this would help us to port other Sciruby gems easily to JRuby in future because then we will be having enough experience with port using similar code style and also we could optimize the code according to our own will.

**Documentation**

The documentation of NMatrix for JRuby would be similar to that for MRI since we are just porting the library.

**Please provide a specific timeline for your project from application period until pencils-down. What benchmarks will you set for yourself? The greater the detail on this question and the previous, the better.**


## Timeline

During the community bonding period, I will study about Apache Commons Math in detail and try to understand and decide upon the best solution for any computational problem. While initially developing my sample code for NMatrix in Java, I used Array2DRowRealMatrix for creating a matrix. The matrix multiplication for two 103 * 103 matrices took me 9.6 seconds. After using MatrixUtils Class to create the same RealMatrix, the multiplication time was reduced to 0.9 seconds. If we use BlockRealMatrix Class we can even speed up the computation.

Class BlockRealMatrix is specially designed to be cache-friendly. Square blocks are stored as small arrays and allow efficient traversal of data both in row major direction and columns major direction, one block at a time. This greatly increases performance for algorithms that use crossed directional loops like multiplication or transposition thereby creating endless possibilities. I will write small code snippets for whatever I am going to do during the coding period, so that I can spend most of my time writing code, rather than reading documents.

I will be interacting with the JRuby team, trying to learn how we can utilize the Graal VM to its maximum potential.



**Coding Period**

**Week 1 - Week 2 (NMatrix Creation for arbitrary dimension)**

The java backend will be added to the existing repo.
Setting up environment for java backend:
Create ext/java folder.
The jar files would in the vendor directory.
In the frontend environment, detecting if jruby is used:
```ruby
  if defined?(RUBY_ENGINE) && RUBY_ENGINE == "jruby"
    require "jar files"
  end
```
Modify Rakefile to add script for tests .

test_helper.rb
```ruby
  if RUBY_PLATFORM  =~ /jruby
     require "java"
  end
```
The naming pattern for java backend would be similar to c backend. For example:
ruby_nmatrix.c
cNMatrix = rb_define_class("NMatrix", rb_cObject)
rb_define_method(cNMatrix, "initialize", (METHOD)nm_init, -1);

ruby_nmatrix.java
```java
Class Nmatrix{
  public int nm_init{
  }
}
```

Nmatrix will be currently implemented only for dense stype. For an arbitrary value of n. I will use the JNmatrix class that will store the elements in an array of required type. I won’t be using generics(analogous to templates in C) for this purpose. I will be using elements object that will contain the elements of a given type. Before storing the elements the type casting would be done. Next, I will implement type-casting by creating a hierarchy of dtypes.
In the java code I can either use the enumerated data-types or a hierarchy to change the dtype object attribute for an NMatrix object.
Create iterators and methods to reshape, slice, etc. that must exist  for an N-dimensional matrix.

**Week 3- Week 5 (NMatrix for 2D)**

I will implement NMatrix creation for 2D matrices.The nmatrix.rb file will contain the parameters provided to create the NMatrix, i.e shape, elements and dtype. For my sample code I have used Java::NMatrix::Linear class which creates the appropriate data container to create a RealMatrix object(dtype: double) and performs Matrix operations. Commonsmathlinear.class interacts with 2-dimensional matrix to do matrix operations.

Apache Commons Math take cares of various dtypes using RealMatrix and Field Matrix:
RealMatrix : It provides support for double dtype.
FieldMatrix : It provides support for Non-Real elements i.e. Field Elements.  Interface FieldElement interfaces Field Elements. All Known Implementing Classes: BigFraction, BigReal, Complex, Dfp, DfpDec, Fraction  . Class Complex implements Complex dtype and Class Dfp and DfpDec implements floats dtype.
These are the steps I am going to follow :
1.  Using Apache Commons:
Implementation of NVector using the following classes:
FieldVector
FieldVectorFormat
ArrayFieldVector
Real Vector
RealVectorFormat
Array Real Vector

Implementation of NMatrix with 2 dimensions will require implementation for Real and Field Matrices using the following classes:
Real Matrix will require the use of following classes:
RealMatrix
RealMatrixFormat
Field Matrix will require the use of following classes:
FieldMatrix
FieldMatrixFormat

2.  Now we need 2D row-major matrices to solve linear equations . Hence, we create a method to convert a 2D matrix to the following object types:
Array2DRowFieldMatrix
Array2DRowRealMatrix

3. Implement the Class RealLinearOperator to implement methods like getRowDimension,    getColumnDimension, operate, isTransposable

4.  Implementation of Diagonal Matrix.

Next I will implementing methods that will be helpful while working with dtypes in NMatrix.
Next implement
BlockFieldMatrix
BlockRealMatrix

After type-casting is done, Common Maths can take care of the matrix operation. The syntax for matrix operators will be similar to current NMatrix implementation on MRI. Also, addition, subtraction, scalar multiplication and vector multiplication be implemented side-by-side and use the same tests as NMatrix for MRI to make sure everything is working fine. Now we’ll have two things to do; overload the binary operators and unary operators and check test cases. I will  use the remaining time as a buffer period to do benchmarking and to resolve conflicts.


**Week 6 ( Mid Term evaluations )**

Deliverables for mid term evaluations: NMatrix creation with support of  arbitrary dimensions of dense stype, dtypes: byte, int, float, double, complex, object; and, binary and unary operators along with tests. This time will also be used for fixing bugs and improve the tests.


**Week 7- Week 9 ( Matrix Decomposition Algorithms )**

I will implement  Matrix Decomposition Algorithms namely, LU, Cholesky, QR, Eigen Decomposition(symmetric matrices only) and SVD. The solve() methods of the DecompositionSolver interface provide by Commons Math support solving linear systems of equations of the form AX=B, either in linear sense or in least square sense. A RealMatrix instance is used to represent the coefficient matrix of the system. Solving the system is a two phase process: first the coefficient matrix is decomposed in some way and then a solver built from the decomposition solves the system. This allows to compute the decomposition and build the solver only once if several systems have to be solved with the same coefficient matrix. Start by decomposing the coefficient matrix A (in this case using LU decomposition) and build a solver. Next create a RealVector array to represent the constant vector B and use solve(RealVector) to solve the system.
Methods to be implemented: Matrix Inverse, isSingular?,  isSymmetric?

**Week 10 - Week 11 (Performance Improvement/ Optimization)**

NMatrix being a scientific library needs to be highly optimized. Nmatrix for MRI has been highly optimized. Therefore, I would like to profile the library and benchmark the functionalities of NMatrix on Jruby and optimize the library to improve performance. This article provides great information on how we can fine tune the performance of a jruby application.

**Week 12 (  Deliverables for final submission )**

NMatrix for JRuby with support for multi-dimensional matrices, dtypes: byte, int, float, double, complex, object and stype: dense. NMatrix for JRuby will support basic algebraic operators and can be used to solve linear equations. It will include tests and documentation.

**What is one long-term vision for something you'd like scientific software to be able to do. Think big picture, not necessarily realistic in the short term.**

I would like the scientific software to decrease the computation time to such an extent that even the largest practical data sets be computed within milli-seconds. Scientific softwares must not make the users wait for the output.

**What are your hobbies, aside from coding? Tell us a little about yourself that isn't reflected in the rest of your application. What do you want to do with your life (if you have any idea)?**

I was brought up in this typical Indian home where studying was the thing that all kids did. As I entered my university I continued to do the same. I discovered coding here. Coding became my hobby and gradually over the years it became my passion. Whenever I am tired and stressed out with coding I turn to movies and TV shows.
In the past three years I have developed a growing interest in the Indian political scenario. I like to watch televised debates between leaders over various issues of national and local importance. I actively follow the policies and bills passed and read on different forums what the public is thinking and come to terms with it by forming my own opinions. This hobby was started quite recently and I would like to develop a critical outlook to comment, critique and suggest changes on a public scale.

Regarding what I want to with my life, I haven’t formed a clear idea in my mind but there is something that drives me towards entrepreneurship. I see myself as CTO of a startup, that is disruptive and actively growing a few years down the line. What the startup will be about and with whom I will be working, I have no idea, but things will work out.


**What else do you think we should have asked but didn't? Propose a question of your own and answer it here.**

**Why should you contribute to open-source software?**

I think open-source software development is about helping the community with high-quality software engineered with the best ideas and methodologies that we can come-up with. The Open-source community continuously comes up with new ideas and tries to make things better.
Also, it’s about how one can become a better programmer. Contributing to Open-source software development teaches me to write better code, learn the best coding practices and the latest software stack. When I first tried to contribute code to BioJavascript, everything seemed too tough. Gradually I began to enjoy it and I learnt a lot.
I feel contributing to open-source adds a lot to my own skills and resume. For example, anyone can use a framework for software development; but it’s challenging to develop one. It is also exciting when you successfully develop a framework, and the community appreciates it.

**Bonus question: One aim of the Ruby Science Foundation (SciRuby) is to increase diversity in open source science software development. How do we get more women interested in open source software development and science? How do we get more people from underrepresented groups involved?**


Ruby Science Foundation could have outreach programs for the underrepresented by setting up 48-hours workshops free-of-cost.

We could use leading content creators of local fame in specific localities to create awareness regarding Sciruby.

We could organise Women-centric coding marathons around the year.

We could have sciruby reps in women universities to create an interest among them.

Tie-up with schools and institutions in marginalised areas for creating awareness about coding in general and Sciruby in particular.

Create video tutorials that are immersive and interactive and collaborate with educational websites like codecademy, udemy, coursera etc. so that we could capture the interest of young minds from diverse groups at a developing age.

