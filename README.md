Download Link: https://assignmentchef.com/product/solved-cs2030s-practical-assessment-2
<br>
<table width="683">

 <tbody>

  <tr>

   <td colspan="3" width="683">Java provides a Random class with a nextInt(int bound) method that returns a random (more precisely pseudorandom), uniformly distributed integer value between 0 (inclusive) and the specified bound (exclusive).Random integer values within the range 0 (inclusive) to Integer.MAX_VALUE (exclusive) can be generated as follows:

    <table width="609">

     <tbody>

      <tr>

       <td width="609">jshell&gt; Random r = new Random(2030) r ==&gt; <a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="3b515a4d5a154e4f525715695a555f54567b0f0e090b5e595a5f">[email protected]</a> jshell&gt; r.nextInt(Integer.MAX_VALUE)$.. ==&gt; 1327734301 jshell&gt; r.nextInt(Integer.MAX_VALUE)$.. ==&gt; 588347554 jshell&gt; r.nextInt(Integer.MAX_VALUE)$.. ==&gt; 1132554824</td>

      </tr>

     </tbody>

    </table>Notice that each time the statement r.nextInt(Integer.MAX_VALUE) is invoked, a different random value is produced. Clearly, some changes in mutable state happens after every invocation of the nextInt method. In order to realize an <em>immutable</em> random number generator, we generate a random integer based on a given seed,

    <table width="609">

     <tbody>

      <tr>

       <td width="609">jshell&gt; new Random(2030).nextInt(Integer.MAX_VALUE) $.. ==&gt; 1327734301</td>

      </tr>

     </tbody>

    </table>and use this new value as the seed to generate the next random value,

    <table width="609">

     <tbody>

      <tr>

       <td width="609">jshell&gt; new Random(new Random(2030).nextInt(Integer.MAX_VALUE)).…&gt; nextInt(Integer.MAX_VALUE)$.. ==&gt; 1503777125</td>

      </tr>

     </tbody>

    </table>Each invocation of the above now returns the same value. Using this technique of seed replacement, the first five random values generated using this method is as follows. We consider the initial seed to be the first random number.</td>

  </tr>

  <tr>

   <td width="37"> </td>

   <td width="609">jshell&gt; int i = 2030 i ==&gt; 2030 jshell&gt; i = new Random(i).nextInt(Integer.MAX_VALUE)i ==&gt; 1327734301 jshell&gt; i = new Random(i).nextInt(Integer.MAX_VALUE)i ==&gt; 1503777125 </td>

   <td width="37"> </td>

  </tr>

 </tbody>

</table>

<table width="609">

 <tbody>

  <tr>

   <td width="609">jshell&gt; Rand.of(2030) instanceof Rand$.. ==&gt; true jshell&gt; Rand.of(2030).get()$.. ==&gt; 2030 jshell&gt; Rand.of(2030).next() instanceof Rand$.. ==&gt; true jshell&gt; Rand.of(2030).next().get()$.. ==&gt; 1327734301 jshell&gt; Rand.of(2030).next().next().get()$.. ==&gt; 1503777125 jshell&gt; Rand r = Rand.of(2030) r ==&gt; Rand jshell&gt; r.get()$.. ==&gt; 2030 jshell&gt; r.next().get()$.. ==&gt; 1327734301 jshell&gt; r.get()$.. ==&gt; 2030 jshell&gt; r.next().next().get()$.. ==&gt; 1503777125 </td>

  </tr>

 </tbody>

</table>

jshell&gt; i = new Random(i).nextInt(Integer.MAX_VALUE)

i ==&gt; 1593627480




jshell&gt; i = new Random(i).nextInt(Integer.MAX_VALUE) i ==&gt; 222432456

<h2>Task</h2>

Your task is to create a context that handles the implementation details of random number generation.

There are altogether five levels. You need to complete ALL levels.

<strong>Take Note!</strong>

Write each class/interface/enum in its own file with meaningful names.

Ensure that ALL object properties and class constants are declared private final.

Ensure that your classes are NOT cyclic dependent.

You are NOT allowed to use the following java keywords/literals: null, instanceof Java reflection is NOT allowed.

There should be NO type cast with SuppressWarnings

There is no restriction on Java libraries. However, if you use java.util.Optional, do not use the get/isPresent/isEmpty methods.

Do not use * wildcard imports.

For ease of implementation, you need NOT include bounded/unbounded wildcards.

Do NOT define anonymous inner classes; define lambdas instead.

Do NOT use method references :: (the grader cannot handle it).

Do NOT use ellipsis, e.g. String…

In essence, keep to the constructs and programming discipline that is instilled throughout the module. Moreover, for brevity in presenting test cases, we do not “type-witness” static methods unless necessary, i.e. Optional.

&lt;Integer&gt;of(1) is more concisely represented as Optional.of(1).

<h2>Level 1</h2>

Define a Rand class to generate random values using the seed replacement technique described above. The Rand class comprises of the following:

a static of method that takes in an integer seed and creates a Rand object

a toString method that simply outputs Rand a get method that returns the random integer value a next method that returns the “next” Rand object

You may assume that the of method is used only at the start of a chain of Rand methods.

<table width="609">

 <tbody>

  <tr>

   <td width="609">jshell&gt; Rand.of(2030).…&gt;     stream().…&gt;     limit(5).…&gt;     forEach(x -&gt; System.out.println(x))2030132773430115037771251593627480222432456jshell&gt; Rand.of(2030).…&gt;     next().…&gt;     stream().…&gt;     limit(5).…&gt;     forEach(x -&gt; System.out.println(x))1327734301150377712515936274802224324561414485811</td>

  </tr>

 </tbody>

</table>

<table width="609">

 <tbody>

  <tr>

   <td width="609">jshell&gt; Function&lt;Integer,Integer&gt; f = x -&gt; x % 10 f ==&gt; $Lambda$19/<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="91a1e9a1a1a1a1a1a1a1a9a1a1a1f0f4f2a5a1d1a5a7f5a4a7f5a7a6">[email protected]</a>jshell&gt; Rand.randRange(2030, f).…&gt;     limit(20).    …&gt;     forEach(x -&gt; System.out.print(x + ” “))0 1 5 0 6 1 0 4 4 2 0 9 1 8 1 5 3 1 3 8</td>

  </tr>

 </tbody>

</table>

<table width="609">

 <tbody>

  <tr>

   <td width="609">jshell&gt; Rand.of(2030).map(x -&gt; x – 1).get()$.. ==&gt; 2029 jshell&gt; Rand.of(2030).next().map(x -&gt; x – 1).get()$.. ==&gt; 1327734300 jshell&gt; Rand.of(2030).map(x -&gt; x – 1).next().get()$.. ==&gt; 1327734300 jshell&gt; Rand.of(2030).next().map(x -&gt; x – 1).next().get()$.. ==&gt; 1503777124jshell&gt; Rand.of(2030).map(x -&gt; x – 1).stream().…&gt;     limit(5).…&gt;     forEach(x -&gt; System.out.print(x % 10 + ” “))9 0 4 9 5  jshell&gt; Rand.of(2030).next().map(x -&gt; x – 1).stream().…&gt;     limit(5).…&gt;     forEach(x -&gt; System.out.print(x % 10 + ” “))0 4 9 5 0  jshell&gt; Rand.of(2030).map(x -&gt; x – 1).next().stream().…&gt;     limit(5).…&gt;     forEach(x -&gt; System.out.print(x % 10 + ” “))</td>

  </tr>

 </tbody>

</table>

jshell&gt; r.get()

$.. ==&gt; 2030

<h2>Level 2</h2>

Random numbers are generated repeatedly during simulations. Include a stream() method to generate a Stream&lt;Integer&gt; of random numbers as shown in the sample run below:

Moreover, generating sequences of random integer values within a specific range is very common. Include a static method randRange that takes in an integer seed, and a Function that maps the random generated values to the specified range.

As an example, the first five random values generated from Rand.of(2030), i.e. 2030, 1327734301, 1503777125, 1593627480, 222432456 can be mapped to the range 0 to 9, by taking the remainder after dividing by 10, i.e. 0, 1, 5, 0, 6.

<h2>Level 3</h2>

Include a method map that maps the random value in the Rand object. Note how the order of method calls to next and map can be interchanged while still generating the same outcome.

<table width="609">

 <tbody>

  <tr>

   <td width="609">0 4 9 5 0  jshell&gt; Rand.of(2030).next().map(x -&gt; x – 1).next().stream().…&gt;     limit(5).…&gt;     forEach(x -&gt; System.out.print(x % 10 + ” “))4 9 5 0 9  jshell&gt; Rand.of(2030).next().map(x -&gt; x % 2 == 0).next().stream().…&gt;     limit(5).…&gt;     forEach(x -&gt; System.out.print(x + ” “)) false true true false true</td>

  </tr>

 </tbody>

</table>

<table width="609">

 <tbody>

  <tr>

   <td width="609">jshell&gt; Rand.randRange(2030, x -&gt; x % 10).…&gt;     limit(5).…&gt;     forEach(System.out::println)01506  jshell&gt; Rand.randRange(2030, x -&gt; String.format(“[%02d]”, x % 100)).…&gt;     limit(5).…&gt;     forEach(System.out::println)[30][01][25][80][56]jshell&gt; double lo = -1.0 lo ==&gt; -1.0 jshell&gt; double hi = 1.0 hi ==&gt; 1.0jshell&gt; // random floating point values from lo to hi, both inclusive.jshell&gt; Rand.…&gt; randRange(2030, x -&gt; (hi – lo) * x / (Integer.MAX_VALUE – 1) + lo).…&gt; limit(10).…&gt; forEach(System.out::println)-0.99999810941517180.236548928764228620.40050158500718090.4841812490338284-0.79284363220710640.31734256848445397 -0.5744591109216763-0.4216896737196386-0.23638053726067820.2196226168606641</td>

  </tr>

 </tbody>

</table>

<table width="609">

 <tbody>

  <tr>

   <td width="609">jshell&gt; Rand.of(2030).…&gt; next().…&gt; map(x -&gt; { System.out.println(“ouch!”); return x; }).…&gt; next()$.. ==&gt; Randjshell&gt; Rand.of(2030).next().…&gt; map(x -&gt; { System.out.println(“ouch!”); return x; }).…&gt; next().    …&gt; get() ouch!$.. ==&gt; 1503777125 jshell&gt; Stream&lt;Integer&gt; ints = Rand.randRange(2030, x -&gt; {…&gt;     System.out.println(“ouch!”); return x; }).…&gt; limit(5)ints ==&gt; <a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="b5dfd4c3d49bc0c1dcd99bc6c1c7d0d4d89be6d9dcd6d0fac5c69184f58684d0d38180d086">[email protected]</a> jshell&gt; ints.forEach(x -&gt; System.out.println(x))</td>

  </tr>

 </tbody>

</table>

Now, modify the randRange method so that it can generate a stream of values of any type.

<table width="609">

 <tbody>

  <tr>

   <td width="609">jshell&gt; Rand.of(2030).map(x -&gt; x / 2).get()$.. ==&gt; 1015 jshell&gt; Rand.of(2030).map(x -&gt; x / 2).next().get()$.. ==&gt; 663867150 jshell&gt; Rand.of(2030).flatMap(x -&gt; Rand.of(x).map(y -&gt; y / 2)).get()$.. ==&gt; 1015 jshell&gt; Rand.of(2030).flatMap(x -&gt; Rand.of(x).map(y -&gt; y / 2)).next().get()$.. ==&gt; 663867150jshell&gt; Rand.of(2030).map(x -&gt; x / 2).next().…&gt; stream().limit(5).forEach(x -&gt; System.out.println(x))663867150751888562796813740111216228707242905jshell&gt; Rand.of(2030).next().flatMap(x -&gt; Rand.of(x).map(y -&gt; y / 2)).…&gt; stream().limit(5).forEach(x -&gt; System.out.println(x))663867150751888562796813740111216228707242905jshell&gt; Rand.of(2030).flatMap(x -&gt; Rand.of(x).next().map(y -&gt; y / 2)).…&gt; stream().limit(5).forEach(x -&gt; System.out.println(x))663867150751888562796813740111216228707242905jshell&gt; Rand.of(2030).flatMap(x -&gt; Rand.of(x).map(y -&gt; y / 2).next()).…&gt; stream().limit(5).forEach(x -&gt; System.out.println(x))663867150751888562796813740111216228707242905jshell&gt; Rand.of(2030).flatMap(x -&gt; Rand.of(x).map(y -&gt; y / 2)).next().…&gt; stream().limit(5).forEach(x -&gt; System.out.println(x))663867150751888562796813740111216228707242905</td>

  </tr>

 </tbody>

</table>

The following are additional sample runs that illustrates the evaluation of a Rand object. ouch! 2030 ouch! 1327734301 ouch! 1503777125 ouch! 1593627480 ouch! 222432456

<h2>Level 4</h2>

So far, we have been generating sequences of individual values. How do we generate say, random lists of two integer elements? We use flatMap!

Let’s first look at how flatMap behaves in the context of individual elements.

Now to generate random lists of two elements each, we need to replace the map function within flatMap.

<table width="609">

 <tbody>

  <tr>

   <td width="609">jshell&gt; Rand.of(2030).…&gt; flatMap(x -&gt; Rand.of(x).map(y -&gt; List.of(x,y))) instanceof Rand$.. ==&gt; truejshell&gt; Rand.of(2030).…&gt; flatMap(x -&gt; Rand.of(x).map(y -&gt; List.of(x,y))).get()$.. ==&gt; [2030, 2030]jshell&gt; Rand.of(2030).…&gt; flatMap(x -&gt; Rand.of(x).map(y -&gt; List.of(x,y))).next().get()$.. ==&gt; [1327734301, 1327734301]jshell&gt; Rand.of(2030).…&gt; flatMap(x -&gt; Rand.of(x).map(y -&gt; List.of(x,y))).…&gt; stream().limit(5).forEach(x -&gt; System.out.println(x))[2030, 2030][1327734301, 1327734301][1503777125, 1503777125][1593627480, 1593627480][222432456, 222432456]</td>

  </tr>

 </tbody>

</table>

<table width="609">

 <tbody>

  <tr>

   <td width="609">jshell&gt; Rand.of(2030).…&gt; flatMap(x -&gt; Rand.of(x).map(y -&gt; List.of(x,y)).next()).…&gt; get() $.. ==&gt; [2030, 1327734301]jshell&gt; Rand.of(2030).…&gt; flatMap(x -&gt; Rand.of(x).map(y -&gt; List.of(x,y)).next()).…&gt; next().…&gt; get()$.. ==&gt; [1327734301, 1503777125]jshell&gt; Rand.of(2030).…&gt; flatMap(x -&gt; Rand.of(x).map(y -&gt; List.of(x,y)).next()).…&gt; stream().limit(5).forEach(x -&gt; System.out.println(x))[2030, 1327734301][1327734301, 1503777125][1503777125, 1593627480][1593627480, 222432456][222432456, 1414485811]</td>

  </tr>

 </tbody>

</table>

<table width="609">

 <tbody>

  <tr>

   <td width="609">jshell&gt; Rand.of(2030).…&gt; flatMap(x -&gt; Rand.of(1010).map(y -&gt; List.of(x,y))).…&gt; stream().limit(5).forEach(x -&gt; System.out.println(x))[2030, 1010][1327734301, 1010][1503777125, 1010][1593627480, 1010][222432456, 1010]jshell&gt; Rand.of(2030).…&gt; flatMap(x -&gt; Rand.of(1010).map(y -&gt; List.of(x,y)).next()).…&gt; stream().limit(5).forEach(x -&gt; System.out.println(x))[2030, 1530112223][1327734301, 1530112223][1503777125, 1530112223][1593627480, 1530112223][222432456, 1530112223]jshell&gt; Rand.of(2030).…&gt; flatMap(x -&gt; Rand.of(x).map(y -&gt; List.&lt;Number&gt;of(x, (y % 10) / 2.0))).…&gt; stream().limit(5).forEach(x -&gt; System.out.println(x))[2030, 0.0][1327734301, 0.5][1503777125, 2.5]</td>

  </tr>

 </tbody>

</table>

The above flatMap operations generates a list of two elements which are the same.

Let’s include a next within the flatMap.

The two values within a list are now consecutive random numbers. Also the first element of a list, is the second element of the previous list. This is the expected behaviour.

Below are some other sample tests.

<table width="609">

 <tbody>

  <tr>

   <td width="609">[1593627480, 0.0][222432456, 3.0]jshell&gt; Stream&lt;Integer&gt; ints = Rand.of(2030).…&gt;     flatMap(x -&gt; {…&gt;         System.out.println(“ouch!”);…&gt;         return Rand.of(x); }).…&gt;     stream().limit(5)ints ==&gt; <a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="4d272c3b2c6338392421633e393f282c20631e21242e28023d3e697c0d782f2e2c2f787c74">[email protected]</a> jshell&gt; ints.forEach(x -&gt; {}) ouch! ouch! ouch! ouch! ouch!  jshell&gt; ints = Rand.of(2030).…&gt;     flatMap(x -&gt; {…&gt;         System.out.println(“ouch!”);…&gt;         return Rand.of(x).map(y -&gt; {…&gt;             System.out.println(“aiyo!”);…&gt;             return y + 1; }); }).…&gt;     stream().limit(5)ints ==&gt; <a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="1973786f78376c6d7075376a6d6b7c7874374a75707a7c56696a3d2859287c2a202e7c7d2e">[email protected]</a> jshell&gt; ints.forEach(x -&gt; System.out.println(x)) ouch! aiyo! 2031 ouch! aiyo! 1327734302 ouch! aiyo! 1503777126 ouch! aiyo! 1593627481 ouch! aiyo! 222432457</td>

  </tr>

 </tbody>

</table>

<h2>Level 5</h2>

Finally, let us use our random number generator for a classic Monte-Carlo simulation — that of estimating the value of pi.

Briefly, we can generate random points within the square region spanning bottom-left (-1,-1) to top-right (1,1), and determine how many of these points fall into the circle centred at (0, 0) with radius 1.0. The proportion of points that falls within the circle will be approximately equals to pi/4.

You are given the Circle and Point classes. Define a Main class with a static method double simulate(int seed, int n) that takes in the seed and the number of simulation trials n. The method generates n number of points within the region (-1,-1) and (1,1), determines how many of these fall within the circle, and returns the estimated value of pi as a double value.

Take note that unlike the levels above, we wish to avoid duplicate random values. Here is a peek on what the first ten points should look like using 2030 as the seed. You may compare this with the random floating point values generated from one of the test cases in level 3.

(-0.9999981094151718, 0.23654892876422862)

(0.4005015850071809, 0.4841812490338284)

(-0.7928436322071064, 0.31734256848445397)

(-0.5744591109216763, -0.4216896737196386)

(-0.2363805372606782, 0.2196226168606641)

(-0.0677647097667351, 0.05293416423065045)

(-0.87413697771182, 0.7369958010846709)

(-0.563276542875242, -0.03873627450199446)

(-0.2820637172852305, -0.46053203051959357)

(0.07041811018289823, -0.8967840819589645)

Below are simulations over an increasing number of trials with the same seed 2030. Notice the convergence to the value of pi.




<table width="683">

 <tbody>

  <tr>

   <td width="37"> </td>

   <td width="609">jshell&gt; Stream.iterate(10, x -&gt; x * 10).…&gt;     limit(6).…&gt;     map(x -&gt; Main.simulate(2030, x)).…&gt;     forEach(x -&gt; System.out.println(x))3.23.03.2243.17883.1513.1474</td>

   <td width="37"> </td>

  </tr>

 </tbody>

</table>