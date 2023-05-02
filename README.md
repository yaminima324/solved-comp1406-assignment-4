Download Link: https://assignmentchef.com/product/solved-comp1406-assignment-4
<br>
This assignment builds a very simple insurance company system.  You will gain  practice with inheritance, overriding methods, an abstract class and abstract

methods.   The insurance system will keep track of the insurance company’s clients. Each client will have at least one policy with the company.  The last part of the assignment is unrelated … and involves creating a simple GUI window.<strong> Changes have been made (shown in yellow) on Feb 15<sup>th</sup>.</strong>




<strong>public </strong>Policy(<strong>float </strong>amt) {         <strong>amount </strong>= amt;

<strong>policyNumber </strong>= <em>NEXT_POLICY_NUMBER</em>++;

}

<strong>public int </strong>getPolicyNumber() { <strong>return </strong><strong>policyNumber</strong>; }     <strong>public float </strong>getAmount() { <strong>return </strong><strong>amount</strong>; }




<strong>public </strong>String toString() {

<strong>return </strong>String.<em>format</em>(<strong>“Policy: %04d amount: $%1.2f”</strong>, <strong>policyNumber</strong>, <strong>amount</strong>);     }

<strong>public boolean </strong>isExpired() {         <strong>return false</strong>;

}

}

Now define a <strong>DepreciatingPolicy</strong> class as a subclass of <strong>Policy</strong> which has the following:

<ul>

 <li>a <strong>private</strong> instance variable called <u>rate</u> of type <strong>float</strong> which represents the rate at which the policy depreciates each time a claim is made. For example, a rate of 0.10 means that the value of the policy (i.e., the amount) depreciates 10% each time a claim is made (we will discuss the making of claims in the next section).</li>

 <li>a <strong>public</strong> constructor which takes a <strong>float</strong> representing the <u>amount</u> and another <strong>float</strong> representing the <u>rate</u>. This constructor <strong>MUST</strong> make full/proper use of inheritance.</li>

 <li>a <strong>public</strong> get method for the <u>rate</u>.</li>

 <li>a <strong>toString()</strong> method that returns a <strong>String</strong> with the following example format:</li>

</ul>

<strong>DepreciatingPolicy: 0001 amount: $320.00 rate: 10.0%</strong>

You <strong>MUST</strong> make use of inheritance by calling the <strong>toString()</strong> from the superclass.   Also, the <u>rate</u> must be properly formatted.

<ul>

 <li>an instance method called <strong>isExpired()</strong> which returns <strong>true</strong> if the <u>amount</u> of this policy has depreciated to <strong>0</strong> (assume a value less than 0.01 is zero). You <strong>MUST</strong> write this method without any IF/SWITCH/TERNARY conditional statements.</li>

 <li>an instance method called <strong>depreciate()</strong> which reduces the <u>amount</u> of the policy by the <u>rate</u> For example, if the amount is <strong>$100</strong> and the rate is <strong>0.10</strong>, then the amount after this method is called should be <strong>$90</strong>.</li>

</ul>

Define an <strong>ExpiringPolicy</strong> class as a subclass of <strong>Policy</strong> which has the following:




<ul>

 <li>a <strong>private</strong> instance variable called <u>expiryDate</u> of type <strong>Date</strong> (from <strong>util.Date</strong> package) that contains the date after which the policy is invalid.</li>

 <li>a <strong>public</strong> constructor which takes a <strong>float</strong> representing the <u>amount</u> and a <strong>Date</strong> representing the <u>expiryDate</u>. This constructor <strong>MUST</strong> make full/proper use of inheritance.</li>

 <li>a <strong>public</strong> constructor which takes a <strong>float</strong> representing the <u>amount</u>. This constructor <strong>MUST</strong> make full/proper use of inheritance.   The <u>expiryDate</u> should then be set to exactly one year after the policy was created.   Here is how you can do this:</li>

</ul>

GregorianCalendar aCalendar = <strong>new</strong> GregorianCalendar();  aCalendar.add(Calendar.YEAR,<strong>1</strong>);  expiryDate = aCalendar.getTime();

<ul>

 <li>a <strong>public</strong> get method for the <u>expiryDate</u>.</li>

 <li>a <strong>toString()</strong> method that makes use of inheritance by calling the <strong>toString()</strong> from the superclass and returns a <strong>String</strong> with the following example format which includes the parentheses (i.e., look at the <strong>SimpleDateFormat</strong> class described in section 13.3 of the course notes in order to see how to format the date properly).   Notice the difference (underlined) between expired and no-expired policies:</li>

</ul>

<strong>ExpiringPolicy: 0001 amount: $320.00 expired on: April 30, 2001 (12:08PM) </strong>

<strong>ExpiringPolicy: 0006 amount: $500.00 expires: May 23, 2023 (4:46AM) </strong>

<ul>

 <li>An instance method called <strong>isExpired()</strong> which returns <strong>true</strong> if the computer’s current date is ON or AFTER the <u>expiryDate</u> and <strong>false</strong> (Hint: the <strong>Date</strong> class has methods <strong>before(Date d)</strong> and <strong>after(Date d)</strong> … see section 13.3 of the course notes).</li>

</ul>




Now test your new classes with the following program:




<strong>import </strong>java.util.*;




<strong>public class </strong>PolicyTester {

<strong>public static void </strong>main(String args[]) {         System.<strong><em>out</em></strong>.println(<strong>new </strong>Policy(320));

DepreciatingPolicy p1 = <strong>new </strong>DepreciatingPolicy(500.1f, 0.1f);

System.<strong><em>out</em></strong>.println(p1);         p1.depreciate();

System.<strong><em>out</em></strong>.println(p1);

System.<strong><em>out</em></strong>.println(<strong>new </strong>ExpiringPolicy(1000));

Date expDate = <strong>new </strong>GregorianCalendar(2021, 0, 2, 23, 59).getTime();

ExpiringPolicy p2 = <strong>new </strong>ExpiringPolicy(2000, expDate);

System.<strong><em>out</em></strong>.println(p2);

System.<strong><em>out</em></strong>.println(p2.isExpired());

expDate = <strong>new </strong>GregorianCalendar(2013, 3, 1, 23, 59).getTime();

ExpiringPolicy p3 = <strong>new </strong>ExpiringPolicy(2000, expDate);

System.<strong><em>out</em></strong>.println(p3);

System.<strong><em>out</em></strong>.println(p3.isExpired());

}

}

Here is the expected output (your date on line 4 will differ):

Policy: 0001 amount: $320.00

DepreciatingPolicy: 0002 amount: $500.10 rate: 10.0%

DepreciatingPolicy: 0002 amount: $450.09 rate: 10.0%

ExpiringPolicy: 0003 amount: $1000.00 expires: May 16, 2018 (01:18PM) ExpiringPolicy: 0004 amount: $2000.00 expires: January 02, 2021 (11:59PM) false

ExpiringPolicy: 0005 amount: $2000.00 expired on: April 01, 2013 (11:59PM) true

____________________________________________________________________________________________

<h1>(2) The <strong>Clients </strong></h1>

We will now define the following hierarchy:




To begin, copy the code from the following <strong>Client</strong> class:




<strong>import </strong>java.util.*;




<strong>public abstract class </strong>Client {

<strong>private static final int </strong><strong><em>MAX_POLICIES_PER_CLIENT </em></strong>= 10;




<strong>private static int </strong><em>NEXT_CLIENT_ID </em>= 1;

<strong>private   </strong>String        <strong>name</strong>;     <strong>private   int           </strong><strong>id</strong>;     <strong>protected </strong>Policy[]      <strong>policies</strong>;     <strong>protected int           </strong><strong>numPolicies</strong>;




<strong>public </strong>Client(String n) {         <strong>name </strong>= n;

<strong>id </strong>= <em>NEXT_CLIENT_ID</em>++;

<strong>policies </strong>= <strong>new </strong>Policy[<strong><em>MAX_POLICIES_PER_CLIENT</em></strong>];         <strong>numPolicies </strong>= 0;

}

<strong>public </strong>String getName() { <strong>return </strong><strong>name</strong>; }     <strong>public int </strong>getId() { <strong>return </strong><strong>id</strong>; }

<strong>public </strong>Policy[] getPolicies() { <strong>return </strong><strong>policies</strong>; }     <strong>public int </strong>getNumPolicies() { <strong>return </strong><strong>numPolicies</strong>; }




<strong>public </strong>String toString() {

<strong>return </strong>String.<em>format</em>(<strong>“Client: %06d amount: %s”</strong>, <strong>id</strong>, <strong>name</strong>);

} }




Create the following in the  <strong>Client</strong> class:

<ul>

 <li>a <strong>public</strong> method called totalCoverage() which returns a <strong>float</strong> containing the total amount of coverage of all the client’s policies.</li>

 <li>a <strong>public</strong> method called addPolicy(<strong>Policy</strong> p) which adds the given <strong>Policy</strong> to the array of policies, provided that the limit has not been reached … and returns the <strong>Policy</strong> object, or <strong>null</strong> if not added.</li>

 <li>a <strong>public</strong> method called openPolicyFor(<strong>float</strong> amt) which creates a new <strong>Policy</strong> for the amount specified in the parameter and adds it to the client using (and returning the result from) the <strong>addPolicy()</strong> method</li>

 <li>a <strong>public</strong> method called openPolicyFor(<strong>float</strong> amt, <strong>float</strong> rate) which creates a new</li>

</ul>

<strong>DepreciatingPolicy</strong> for the amount and rate specified in the parameters and adds it to the client using (and returning the result from) the <strong>addPolicy()</strong> method.

<ul>

 <li>a <strong>public</strong> method called openPolicyFor(<strong>float</strong> amt, Date expire) which creates a new</li>

</ul>

<strong>ExpiringPolicy</strong> for the amount and expiry date specified in the parameters and adds it to the client using (and returning the result from) the addPolicy() method above.

<ul>

 <li>a <strong>public</strong> method called getPolicy(<strong>int</strong> polNum) which examines all <strong>Policy</strong> objects in <u>policies</u>. If one is found whose <u>policyNumber</u> matches the input parameter, then it should be returned by the method. Otherwise <strong>null</strong> is returned.</li>

 <li>a <strong>public</strong> method called cancelPolicy(<strong>int</strong> polNum) which removes the police from the client’s list with the given policy number, if found. It should return true if the policy was found, otherwise it should return false.   When a policy is removed from the array, the empty location in the array should be replaced by the last policy in the array.</li>

 <li>a <strong>public</strong> <strong>abstract</strong> method called makeClaim(<strong>int</strong> polNum) that returns a</li>

</ul>

Now create the two subclasses of <strong>Client</strong>, one called <strong>IndividualClient</strong> and the other called

<strong>CompanyClient</strong>.    Try compiling them.   Notice that your test code will not compile.   That’s because subclasses DO NOT inherit constructors and java requires a constructor to be available. Do the following:

<ul>

 <li>Create a constructor (taking a single String argument) for each of these subclasses that calls the one in <strong>Client</strong>.</li>

 <li>Go back and alter your <strong>toString()</strong> method in <strong>Client</strong> class so that the proper client type is displayed. For example:   CompanyClient 0001: Bob B. Pins     To do this, you will want</li>

</ul>

to figure out how to get the name of the class as a String.   (<u>hint</u>: type <strong><sub>this.</sub></strong> and then let IntelliJ show a list of available methods.  You need to find out what class you have and then find out the name of the class).

<ul>

 <li>Implement the makeClaim(<strong>int</strong> polNum) method in the <strong><sub>IndividualClient</sub></strong> If the policy with that number is not found or has expired, then nothing is to be done, just return <strong>0</strong>.   <strong>IndividualClients</strong> are allowed to make only 1 claim per regular <strong>Policy</strong> but <strong>DepreciatingPolicy</strong>s and</li>

</ul>

<strong>ExpiringPolicy</strong>s can have multiple claims.   So, you should cancel a regular policy after a claim is made on it.   If the claim is being made for a <strong>DepreciatingPolicy</strong>, then you must make sure to depreciate the policy.   This method should return the amount of the policy (amount after depreciating in the case of <strong>DepreciatingPolicy</strong>s) if the claim was made ok, otherwise 0 is returned.

<ul>

 <li>In the <strong>Policy</strong> class, implement a method called handleClaim() that returns the amount of the policy.</li>

 <li>In the <strong>DepreciatingPolicy</strong> class, implement handleClaim() so that it returns the amount of the policy but also depreciates the policy. Note that the amount returned is the amount of the policy before it was depreciated.</li>

 <li>In the <strong>ExpiringPolicy</strong> class, implement handleClaim() so that it returns the amount of the policy as long as the policy has not yet expired, otherwise it returns 0.</li>

 <li>In the <strong>CompanyClient</strong> class, implement the makeClaim(<strong>int</strong> polNum) method so that it first checks to make sure the policy is one belonging to this client and then uses the double-dispatching technique by calling the handleClaim() You <strong>MUST NOT</strong> use any IF statements to determine the policy type … that’s would undo the advantages of double-dispatching.  Note that <strong>CompanyClients</strong> DO NOT have their policy removed afterwards, and so you should make use of the getPolicy() method.   If no policy is found with the given <strong>polNum</strong>, return 0;</li>

</ul>




____________________________________________________________________________________________ (3) Testing

Now test what you have done with the following program:

<strong>import </strong>java.util.GregorianCalendar;




<strong>public class </strong>ClientTester {     <strong>public static void </strong>main(String args[]) {

<em>// Create an individual client, open some policies and then make some claims </em>

<em>        </em>IndividualClient ic = <strong>new </strong>IndividualClient(<strong>“Bob B. Pins”</strong>);         ic.openPolicyFor(100);         ic.openPolicyFor(200, 0.10f);

ic.openPolicyFor(300, <strong>new </strong>GregorianCalendar(2020, 0, 2, 23, 59).getTime());         ic.openPolicyFor(400, <strong>new </strong>GregorianCalendar(2009, 5, 4, 12, 00).getTime());

Policy p = <strong>new </strong>Policy(500);




System.<strong><em>out</em></strong>.println(<strong>“Here are the Individual Client’s policies:”</strong>);         <strong>for </strong>(<strong>int </strong>i=0; i&lt;ic.getNumPolicies(); i++)

System.<strong><em>out</em></strong>.println(<strong>”  ” </strong>+ ic.getPolicies()[i]);




System.<strong><em>out</em></strong>.println(<strong>“Making claims:”</strong>);

System.<strong><em>out</em></strong>.println(String.<em>format</em>(<strong>”  Claim for policy 0001: $%6.2f”</strong>,ic.makeClaim(1)));

System.<strong><em>out</em></strong>.println(String.<em>format</em>(<strong>”  Claim for policy 0002: $%6.2f”</strong>,ic.makeClaim(2)));

System.<strong><em>out</em></strong>.println(String.<em>format</em>(<strong>”  Claim for policy 0003: $%6.2f”</strong>,ic.makeClaim(3)));

System.<strong><em>out</em></strong>.println(String.<em>format</em>(<strong>”  Claim for policy 0004: $%6.2f”</strong>,ic.makeClaim(4)));         System.<strong><em>out</em></strong>.println(String.<em>format</em>(<strong>”  Claim for policy 0005: $%6.2f”</strong>,ic.makeClaim(5)));




System.<strong><em>out</em></strong>.println(<strong>“Here are the Individual Client’s policies after claims:”</strong>);         <strong>for </strong>(<strong>int </strong>i=0; i&lt;ic.getNumPolicies(); i++)

System.<strong><em>out</em></strong>.println(<strong>”  ” </strong>+ ic.getPolicies()[i]);




System.<strong><em>out</em></strong>.println(String.<em>format</em>(<strong>“The total policy coverage for this client: $%1.2f”</strong>,

ic.totalCoverage()));




<em>// Create a company client, open some policies and then make some claims </em>

<em>        </em>CompanyClient cc = <strong>new </strong>CompanyClient(<strong>“The Pillow Factory”</strong>);         cc.openPolicyFor(1000);         cc.openPolicyFor(2000, 0.10f);

cc.openPolicyFor(3000, <strong>new </strong>GregorianCalendar(2020, 0, 2, 23, 59).getTime());         cc.openPolicyFor(4000, <strong>new </strong>GregorianCalendar(2009, 5, 4, 12, 00).getTime());




System.<strong><em>out</em></strong>.println(<strong>“</strong><strong>
</strong><strong>Here are the Company Client’s policies:”</strong>);         <strong>for </strong>(<strong>int </strong>i=0; i&lt;cc.getNumPolicies(); i++)

System.<strong><em>out</em></strong>.println(<strong>”  ” </strong>+ cc.getPolicies()[i]);




System.<strong><em>out</em></strong>.println(<strong>“Making claims:”</strong>);

System.<strong><em>out</em></strong>.println(String.<em>format</em>(<strong>”  Claim for policy 0006: $%7.2f”</strong>,cc.makeClaim(6)));

System.<strong><em>out</em></strong>.println(String.<em>format</em>(<strong>”  Claim for policy 0007: $%7.2f”</strong>,cc.makeClaim(7)));

System.<strong><em>out</em></strong>.println(String.<em>format</em>(<strong>”  Claim for policy 0008: $%7.2f”</strong>,cc.makeClaim(8)));

System.<strong><em>out</em></strong>.println(String.<em>format</em>(<strong>”  Claim for policy 0009: $%7.2f”</strong>,cc.makeClaim(9)));         System.<strong><em>out</em></strong>.println(String.<em>format</em>(<strong>”  Claim for policy 0005: $%7.2f”</strong>,cc.makeClaim(5)));




System.<strong><em>out</em></strong>.println(<strong>“Here are the Company Client’s policies after claims:”</strong>);         <strong>for </strong>(<strong>int </strong>i=0; i&lt;cc.getNumPolicies(); i++)

System.<strong><em>out</em></strong>.println(<strong>”  ” </strong>+ cc.getPolicies()[i]);




System.<strong><em>out</em></strong>.println(String.<em>format</em>(<strong>“The total policy coverage for this client: $%1.2f”</strong>,

cc.totalCoverage()));




System.<strong><em>out</em></strong>.println(<strong>“Cancelling policy #12 … did it work: ” </strong>+ cc.cancelPolicy(12));

System.<strong><em>out</em></strong>.println(<strong>“Cancelling policy #8 … did it work: ” </strong>+ cc.cancelPolicy(8));




System.<strong><em>out</em></strong>.println(String.<em>format</em>(<strong>“The total policy coverage for this client: $%1.2f”</strong>,

cc.totalCoverage()));

}

}

Here is the expected output:

Here are the Individual Client’s policies:

<h2>  Policy: 0001 amount: $100.00   DepreciatingPolicy: 0002 amount: $200.00 rate: 10.0%   ExpiringPolicy: 0003 amount: $300.00 expires: January 02, 2020 (11:59PM)   ExpiringPolicy: 0004 amount: $400.00 expired on: June 04, 2009 (12:00PM)</h2>

Making claims:

Claim for policy 0001: $<strong>100.00</strong>

Claim for policy 0002: $<strong>180.00</strong>

Claim for policy 0003: $<strong>300.00</strong>

Claim for policy 0004: $<strong>  0.00 </strong>

Claim for policy 0005: $<strong>  0.00</strong>

Here are the Individual Client’s policies after claims:

<h2>  ExpiringPolicy: 0004 amount: $400.00 expired on: June 04, 2009 (12:00PM)   DepreciatingPolicy: 0002 amount: $180.00 rate: 10.0%   ExpiringPolicy: 0003 amount: $300.00 expires: January 02, 2020 (11:59PM)</h2>

The total policy coverage for this client: <strong>$880.00</strong>




Here are the Company Client’s policies:

<h2>  Policy: 0006 amount: $1000.00   DepreciatingPolicy: 0007 amount: $2000.00 rate: 10.0%   ExpiringPolicy: 0008 amount: $3000.00 expires: January 02, 2020 (11:59PM)   ExpiringPolicy: 0009 amount: $4000.00 expired on: June 04, 2009 (12:00PM)</h2>

Making claims:

Claim for policy 0006: $<strong>1000.00</strong>

Claim for policy 0007: $<strong>2000.00</strong>

Claim for policy 0008: $<strong>3000.00</strong>

Claim for policy 0009: $   <strong>0.00</strong>

Claim for policy 0005: $<strong>   </strong><strong>0.00</strong>

Here are the Company Client’s policies after claims:

<h2>  Policy: 0006 amount: $1000.00   DepreciatingPolicy: 0007 amount: $1800.00 rate: 10.0%   ExpiringPolicy: 0008 amount: $3000.00 expires: January 02, 2020 (11:59PM)   ExpiringPolicy: 0009 amount: $4000.00 expired on: June 04, 2009 (12:00PM)</h2>

The total policy coverage for this client: $<strong>9800.00</strong>

Cancelling policy #12 … did it work: <strong>false</strong>

Cancelling policy #8 … did it work: <strong>true</strong>

The total policy coverage for this client: $<strong>6800.00</strong>

____________________________________________________________________________________________

<h1>(4) A GUI</h1>

Define a class called <strong>AlarmApp</strong> that creates the following window by laying the components out manually using <strong>relocate()</strong> and <strong>setPrefSize()</strong>:




<img decoding="async" data-recalc-dims="1" data-src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2018/03/247.png?w=980&amp;ssl=1" class="aligncenter lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

 <noscript>

  <img decoding="async" class="aligncenter" src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2018/03/247.png?w=980&amp;ssl=1" data-recalc-dims="1">

 </noscript>










Note that the GUI MUST contain the following:

<ul>

 <li>a white background <strong>Pane</strong> (i.e., <strong>“-fx-background-color: white;”</strong>),</li>

 <li>three inner <strong>Pane</strong> objects with borders (i.e., <strong>“-fx-background-color: white; -fx-border-color: gray; -fx-padding: 4 4;”</strong>),</li>

 <li><strong>Labels</strong> on those bordered panes (i.e., <strong>“-fx-background-color: white; -fx-translate-y: -8; fx-translate-x: 10;”</strong>),</li>

 <li>a large (e.g., 48px or anything reasonable) system font <strong>Label</strong> with a dark green color in the “Remaining Time” pane,</li>

 <li>right-aligned <strong>TextFields</strong> in the <u>Current Time</u> and <u>Alarm Time</u> panes with the given times shown,</li>

 <li>a <strong>ComboBox</strong> with prompt text “Select Alarm” and it should contain 3 entries: “Weekday”, “Saturday” and “Sunday”,</li>

 <li>three <strong>Buttons</strong>,</li>

 <li>and two <strong>RadioButtons</strong> belonging to the same <strong>ToggleGroup</strong>.</li>

</ul>




The dimensions of everything is as follows:

<img decoding="async" data-recalc-dims="1" data-src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2018/03/606.png?w=980&amp;ssl=1" class="aligncenter lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

 <noscript>

  <img decoding="async" class="aligncenter" src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2018/03/606.png?w=980&amp;ssl=1" data-recalc-dims="1">

 </noscript>