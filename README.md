Download Link: https://assignmentchef.com/product/solved-ceng351-assignment2
<br>
In this programming assignment, your task is to create a lab entry system that will be used to keep track of students that entered our laboratories. You will use extendible hashing structure to store the students. For detailed description, please refer to <strong>10.2 EXTENDIBLE HASHING chapter in Database Management Systems </strong>(by Raghu Ramakrishnan and Johannes Gehrke) book. Although extendible hashing in the lecture notes uses the first k bits, we will use a different flavor (the last k bits) in this assignment.

The lab entry system is summarized as follows:

<ul>

 <li>Students enter the laboratory by showing their ID cards to our lab entrance system.</li>

 <li>When a student enters the laboratory, we store his/her studentID (i.e., ”e1234567”).</li>

 <li>StudentIDs are stored in extendible hashing structure.</li>

 <li>When a student leaves the laboratory, we remove the related studentID from the system.</li>

</ul>

<h1>1           The Work</h1>

Only four functions and a constructor in the file LabDB.java are needed to be written. You are allowed to add public private members. In addition you are free to add additional classes.

<h2>1.1         public LabDB(int bucketSize)</h2>

Bucket size is defined as the number of entries that a bucket can store. Initialize an extendible hashing structure whose <strong>global depth </strong>(length of common hash <strong>suffix </strong>of bucket address table) is <strong>1 </strong>and and bucket size is given as input parameter.

<h2>1.2         public void enter(String studentID)</h2>

In this function, store the studentID in the extendible hashing structure.

<ul>

 <li>The studentID is in the form e{numeric part}. (i.e., e1234567)</li>

 <li>While locating the studentIDs, use suffix of binary equivalent of the {numeric part} of the studentIDs but store the whole studentID(i.e, e1234567).</li>

</ul>

<h2>1.3         public void leave(String studentID)</h2>

Remove the given studentID from the extendible hashing structure. After removing the studentID please check the following conditions:

<ul>

 <li>If a bucket is empty and its <strong>local depth </strong>(length of common hash <strong>suffix </strong>of data bucket ) is same as its buddy bucket’s (which is referred as ”split image” in the textbook) local depth, then merge the bucket with its buddy bucket and decrease its local depth.</li>

 <li>If all of the buckets’ local depth are less then the global depth, then halve the directory and reduce the global depth.</li>

</ul>

<h2>1.4         public String search(String studentID)</h2>

Search the given studentID in the extendible hashing structure. If the student exists, then return the bucket address (hash suffix) of the bucket that contains the student. If the given studentId does not exist, then return ”-1”. Output samples for this function are given in the Examples section.

<h2>1.5         public void printLab()</h2>

Print the extendible hashing structure to the screen. Output samples for this function are given in the Examples section. Since the grading will be black-box, you should <strong>strictly </strong>obey the sample output.

<h1>2           Examples</h1>

<ul>

 <li>In the examples given below, represents a single <strong>space </strong></li>

 <li>Suppose that bucket size is given as 4 initially. (Please note that, I may test different bucket sizes while evaluating your code.)</li>

</ul>

<table width="119">

 <tbody>

  <tr>

   <td width="119">printLab()</td>

  </tr>

  <tr>

   <td width="119">Global depth <u>: </u>10   <u>: </u>[Local depth:1]1   <u>: </u>[Local depth:1]</td>

  </tr>

 </tbody>

</table>

<ul>

 <li>The student e4 enters the lab.</li>

</ul>

<table width="149">

 <tbody>

  <tr>

   <td width="149">printLab()</td>

  </tr>

  <tr>

   <td width="149">Global depth <u>: </u>10   <u>: </u>[Local depth:1]<em>&lt;</em>e4<em>&gt;</em>1   <u>: </u>[Local depth:1]</td>

  </tr>

 </tbody>

</table>

<ul>

 <li>The students enter the lab with the following order: e12, e32, e16, e1, e5, e21, e10, e15, e7, e19.</li>

</ul>

<table width="266">

 <tbody>

  <tr>

   <td width="266">printLab()</td>

  </tr>

  <tr>

   <td width="266">Global depth <u>: </u>200   <u>: </u>[Local depth:2]<em>&lt;</em>e4<em>&gt;&lt;</em>e12<em>&gt;&lt;</em>e32<em>&gt;&lt;</em>e16<em>&gt;</em>01   <u>: </u>[Local depth:2]<em>&lt;</em>e1<em>&gt;&lt;</em>e5<em>&gt;&lt;</em>e21<em>&gt;</em>10   <u>: </u>[Local depth:2]<em>&lt;</em>e10<em>&gt;</em>11   <u>: </u>[Local depth:2]<em>&lt;</em>e15<em>&gt;&lt;</em>e7<em>&gt;&lt;</em>e19<em>&gt;</em></td>

  </tr>

 </tbody>

</table>

<ul>

 <li>Search for student e21.</li>

</ul>

<table width="232">

 <tbody>

  <tr>

   <td width="232">System.out.println(labdb.search(”e21”))</td>

  </tr>

  <tr>

   <td width="232">01</td>

  </tr>

 </tbody>

</table>

<ul>

 <li>Student e13 enters the lab.</li>

</ul>

<table width="266">

 <tbody>

  <tr>

   <td width="266">printLab()</td>

  </tr>

  <tr>

   <td width="266">Global depth <u>: </u>200   <u>: </u>[Local depth:2]<em>&lt;</em>e4<em>&gt;&lt;</em>e12<em>&gt;&lt;</em>e32<em>&gt;&lt;</em>e16<em>&gt;</em>01   <u>: </u>[Local depth:2]<em>&lt;</em>e1<em>&gt;&lt;</em>e5<em>&gt;&lt;</em>e21<em>&gt;&lt;</em>e13<em>&gt;</em>10   <u>: </u>[Local depth:2]<em>&lt;</em>e10<em>&gt;</em>11   <u>: </u>[Local depth:2]<em>&lt;</em>e15<em>&gt;&lt;</em>e7<em>&gt;&lt;</em>e19<em>&gt;</em></td>

  </tr>

 </tbody>

</table>

<ul>

 <li>Student e20 enters the lab.</li>

</ul>

<table width="266">

 <tbody>

  <tr>

   <td width="266">printLab()</td>

  </tr>

  <tr>

   <td width="266">Global depth <u>: </u>3000 <u>: </u>[Local depth:3]<em>&lt;</em>e32<em>&gt;&lt;</em>e16<em>&gt;</em>001 <u>: </u>[Local depth:2]<em>&lt;</em>e1<em>&gt;&lt;</em>e5<em>&gt;&lt;</em>e21<em>&gt;&lt;</em>e13<em>&gt;</em>010 <u>: </u>[Local depth:2]<em>&lt;</em>e10<em>&gt;</em>011 <u>: </u>[Local depth:2]<em>&lt;</em>e15<em>&gt;&lt;</em>e7<em>&gt;&lt;</em>e19<em>&gt;</em>100  <u>: </u>[Local depth:3]<em>&lt;</em>e4<em>&gt;&lt;</em>e12<em>&gt;&lt;</em>e20<em>&gt;</em>101  <u>: </u>[Local depth:2]<em>&lt;</em>e1<em>&gt;&lt;</em>e5<em>&gt;&lt;</em>e21<em>&gt;&lt;</em>e13<em>&gt;</em>110  <u>: </u>[Local depth:2]<em>&lt;</em>e10<em>&gt;</em>111  <u>: </u>[Local depth:2]<em>&lt;</em>e15<em>&gt;&lt;</em>e7<em>&gt;&lt;</em>e19<em>&gt;</em></td>

  </tr>

 </tbody>

</table>

<ul>

 <li>Student e9 enters the lab.</li>

</ul>

<table width="236">

 <tbody>

  <tr>

   <td width="236">printLab()</td>

  </tr>

  <tr>

   <td width="236">Global depth <u>: </u>3000 <u>: </u>[Local depth:3]<em>&lt;</em>e32<em>&gt;&lt;</em>e16<em>&gt;</em>001 <u>: </u>[Local depth:3]<em>&lt;</em>e1<em>&gt;&lt;</em>e9<em>&gt;</em>010 <u>: </u>[Local depth:2]<em>&lt;</em>e10<em>&gt;</em>011 <u>: </u>[Local depth:2]<em>&lt;</em>e15<em>&gt;&lt;</em>e7<em>&gt;&lt;</em>e19<em>&gt;</em>100              <u>: </u>[Local depth:3]<em>&lt;</em>e4<em>&gt;&lt;</em>e12<em>&gt;&lt;</em>e20<em>&gt;</em>101              <u>: </u>[Local depth:3]<em>&lt;</em>e5<em>&gt;&lt;</em>e21<em>&gt;&lt;</em>e13<em>&gt; </em>110 <u>: </u>[Local depth:2]<em>&lt;</em>e10<em>&gt;</em>111 <u>: </u>[Local depth:2]<em>&lt;</em>e15<em>&gt;&lt;</em>e7<em>&gt;&lt;</em>e19<em>&gt;</em></td>

  </tr>

 </tbody>

</table>

<ul>

 <li>Search for non-existent student.</li>

</ul>

<table width="257">

 <tbody>

  <tr>

   <td width="257">System.out.println(labdb.search(”e101010”))</td>

  </tr>

  <tr>

   <td width="257">-1</td>

  </tr>

 </tbody>

</table>

<ul>

 <li>Search for student e16.</li>

</ul>

<table width="232">

 <tbody>

  <tr>

   <td width="232">System.out.println(labdb.search(”e16”))</td>

  </tr>

  <tr>

   <td width="232">000</td>

  </tr>

 </tbody>

</table>

<ul>

 <li>Student e32 leaves the lab.</li>

</ul>

<table width="236">

 <tbody>

  <tr>

   <td width="236">printLab()</td>

  </tr>

  <tr>

   <td width="236">Global depth <u>: </u>3000 <u>: </u>[Local depth:3]<em>&lt;</em>e16<em>&gt;</em>001 <u>: </u>[Local depth:3]<em>&lt;</em>e1<em>&gt;&lt;</em>e9<em>&gt;</em>010 <u>: </u>[Local depth:2]<em>&lt;</em>e10<em>&gt;</em>011 <u>: </u>[Local depth:2]<em>&lt;</em>e15<em>&gt;&lt;</em>e7<em>&gt;&lt;</em>e19<em>&gt;</em>100              <u>: </u>[Local depth:3]<em>&lt;</em>e4<em>&gt;&lt;</em>e12<em>&gt;&lt;</em>e20<em>&gt;</em>101              <u>: </u>[Local depth:3]<em>&lt;</em>e5<em>&gt;&lt;</em>e21<em>&gt;&lt;</em>e13<em>&gt; </em>110 <u>: </u>[Local depth:2]<em>&lt;</em>e10<em>&gt;</em>111 <u>: </u>[Local depth:2]<em>&lt;</em>e15<em>&gt;&lt;</em>e7<em>&gt;&lt;</em>e19<em>&gt;</em></td>

  </tr>

 </tbody>

</table>

<ul>

 <li>Student e16 leaves the lab.</li>

</ul>

<strong>NOTE: </strong>Bucket 000 becomes empty. Its local depth and its buddy bucket’s(100) local depth are both 3. After deleting e16, merge 000 and its buddy bucket (100) and decrease the local depth.

<table width="236">

 <tbody>

  <tr>

   <td width="236">printLab()</td>

  </tr>

  <tr>

   <td width="236">Global depth <u>: </u>3000 <u>: </u>[Local depth:2]<em>&lt;</em>e4<em>&gt;&lt;</em>e12<em>&gt;&lt;</em>e20<em>&gt;</em>001 <u>: </u>[Local depth:3]<em>&lt;</em>e1<em>&gt;&lt;</em>e9<em>&gt;</em>010 <u>: </u>[Local depth:2]<em>&lt;</em>e10<em>&gt;</em>011 <u>: </u>[Local depth:2]<em>&lt;</em>e15<em>&gt;&lt;</em>e7<em>&gt;&lt;</em>e19<em>&gt;</em>100              <u>: </u>[Local depth:2]<em>&lt;</em>e4<em>&gt;&lt;</em>e12<em>&gt;&lt;</em>e20<em>&gt;</em>101              <u>: </u>[Local depth:3]<em>&lt;</em>e5<em>&gt;&lt;</em>e21<em>&gt;&lt;</em>e13<em>&gt; </em>110 <u>: </u>[Local depth:2]<em>&lt;</em>e10<em>&gt;</em>111 <u>: </u>[Local depth:2]<em>&lt;</em>e15<em>&gt;&lt;</em>e7<em>&gt;&lt;</em>e19<em>&gt;</em></td>

  </tr>

 </tbody>

</table>

<ul>

 <li>Student e10 leaves the lab.</li>

</ul>

<strong>NOTE: </strong>Bucket 10 becomes empty. Its local depth and its buddy bucket’s( 00) local depth are both 2. After deleting e10, merge 10 and its buddy bucket( 00) and decrease the local depth.

<table width="236">

 <tbody>

  <tr>

   <td width="236">printLab()</td>

  </tr>

  <tr>

   <td width="236">Global depth <u>: </u>3000 <u>: </u>[Local depth:1]<em>&lt;</em>e4<em>&gt;&lt;</em>e12<em>&gt;&lt;</em>e20<em>&gt; </em>001 <u>: </u>[Local depth:3]<em>&lt;</em>e1<em>&gt;&lt;</em>e9<em>&gt;</em>010 <u>: </u>[Local depth:1]<em>&lt;</em>e4<em>&gt;&lt;</em>e12<em>&gt;&lt;</em>e20<em>&gt;</em>011 <u>: </u>[Local depth:2]<em>&lt;</em>e15<em>&gt;&lt;</em>e7<em>&gt;&lt;</em>e19<em>&gt;</em>100  <u>: </u>[Local depth:1]<em>&lt;</em>e4<em>&gt;&lt;</em>e12<em>&gt;&lt;</em>e20<em>&gt;</em>101  <u>: </u>[Local depth:3]<em>&lt;</em>e5<em>&gt;&lt;</em>e21<em>&gt;&lt;</em>e13<em>&gt;</em>110  <u>: </u>[Local depth:1]<em>&lt;</em>e4<em>&gt;&lt;</em>e12<em>&gt;&lt;</em>e20<em>&gt;</em>111  <u>: </u>[Local depth:2]<em>&lt;</em>e15<em>&gt;&lt;</em>e7<em>&gt;&lt;</em>e19<em>&gt;</em></td>

  </tr>

 </tbody>

</table>

<ul>

 <li>Student e9 leaves the lab.</li>

</ul>

<table width="236">

 <tbody>

  <tr>

   <td width="236">printLab()</td>

  </tr>

  <tr>

   <td width="236">Global depth <u>: </u>3000 <u>: </u>[Local depth:1]<em>&lt;</em>e4<em>&gt;&lt;</em>e12<em>&gt;&lt;</em>e20<em>&gt; </em>001 <u>: </u>[Local depth:3]<em>&lt;</em>e1<em>&gt;</em>010 <u>: </u>[Local depth:1]<em>&lt;</em>e4<em>&gt;&lt;</em>e12<em>&gt;&lt;</em>e20<em>&gt;</em>011 <u>: </u>[Local depth:2]<em>&lt;</em>e15<em>&gt;&lt;</em>e7<em>&gt;&lt;</em>e19<em>&gt;</em>100  <u>: </u>[Local depth:1]<em>&lt;</em>e4<em>&gt;&lt;</em>e12<em>&gt;&lt;</em>e20<em>&gt;</em>101  <u>: </u>[Local depth:3]<em>&lt;</em>e5<em>&gt;&lt;</em>e21<em>&gt;&lt;</em>e13<em>&gt;</em>110  <u>: </u>[Local depth:1]<em>&lt;</em>e4<em>&gt;&lt;</em>e12<em>&gt;&lt;</em>e20<em>&gt;</em>111  <u>: </u>[Local depth:2]<em>&lt;</em>e15<em>&gt;&lt;</em>e7<em>&gt;&lt;</em>e19<em>&gt;</em></td>

  </tr>

 </tbody>

</table>

<ul>

 <li>Student e1 leaves the lab.</li>

</ul>

<strong>NOTE: </strong>Bucket 001 becomes empty. Its local depth and its buddy bucket’s(101) local depth are both 3. After deleting e1, merge 001 and its buddy bucket(101) and decrease the local depth.

<strong>NOTE2: </strong>After decreasing the local depth, all of the buckets’ local depth are less then the global depth. So we halve the directory and reduce the global depth.

<table width="229">

 <tbody>

  <tr>

   <td width="229">printLab()</td>

  </tr>

  <tr>

   <td width="229">Global depth <u>: </u>200   <u>: </u>[Local depth:1]<em>&lt;</em>e4<em>&gt;&lt;</em>e12<em>&gt;&lt;</em>e20<em>&gt;</em>01   <u>: </u>[Local depth:2]<em>&lt;</em>e5<em>&gt;&lt;</em>e21<em>&gt;&lt;</em>e13<em>&gt;</em>10   <u>: </u>[Local depth:1]<em>&lt;</em>e4<em>&gt;&lt;</em>e12<em>&gt;&lt;</em>e20<em>&gt;</em>11   <u>: </u>[Local depth:2]<em>&lt;</em>e15<em>&gt;&lt;</em>e7<em>&gt;&lt;</em>e19<em>&gt;</em></td>

  </tr>

 </tbody>

</table>

<ul>

 <li>Students e4, e12 and e20 leave the lab respectively.</li>

</ul>

<table width="229">

 <tbody>

  <tr>

   <td width="229">printLab()</td>

  </tr>

  <tr>

   <td width="229">Global depth <u>: </u>200                  <u>: </u>[Local depth:1]01                  <u>: </u>[Local depth:2]<em>&lt;</em>e5<em>&gt;&lt;</em>e21<em>&gt;&lt;</em>e13<em>&gt; </em>10 <u>: </u>[Local depth:1]11 <u>: </u>[Local depth:2]<em>&lt;</em>e15<em>&gt;&lt;</em>e7<em>&gt;&lt;</em>e19<em>&gt;</em></td>

  </tr>

 </tbody>

</table>

<ul>

 <li>Students e5 and e21 leave the lab respectively.</li>

</ul>

<table width="229">

 <tbody>

  <tr>

   <td width="229">printLab()</td>

  </tr>

  <tr>

   <td width="229">Global depth <u>: </u>200   <u>: </u>[Local depth:1]01   <u>: </u>[Local depth:2]<em>&lt;</em>e13<em>&gt;</em>10   <u>: </u>[Local depth:1]11   <u>: </u>[Local depth:2]<em>&lt;</em>e15<em>&gt;&lt;</em>e7<em>&gt;&lt;</em>e19<em>&gt;</em></td>

  </tr>

 </tbody>

</table>

<ul>

 <li>Student e13 leaves the lab.</li>

</ul>

<strong>NOTE: </strong>Bucket 01 becomes empty. Its local depth and its buddy bucket’s(11) local depth are both 2. After deleting e13, merge 01 and its buddy bucket(11) and decrease the local depth.

<strong>NOTE2: </strong>After decreasing the local depth, all of the buckets’ local depth are less then the global depth. So we halve the directory and reduce the global depth.

<table width="223">

 <tbody>

  <tr>

   <td width="223">printLab()</td>

  </tr>

  <tr>

   <td width="223">Global depth <u>: </u>10   <u>: </u>[Local depth:1]1   <u>: </u>[Local depth:1]<em>&lt;</em>e15<em>&gt;&lt;</em>e7<em>&gt;&lt;</em>e19<em>&gt;</em></td>

  </tr>

 </tbody>

</table>