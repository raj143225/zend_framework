#RapidFunnel Coding Specification Update

##1.Documenting using PHP doc­blocks 
Doc­blocks are multi­line comments that precede the definition of classes, attribute variables 
and methods using an uniform pre­defined format. Their purpose is to provide a succinct 
indication of the significance of the object (and implementation where relevant). They should be 
referred to by developers when working with documented entities and the use of specific 
notation allows for the automatic generation documentation for the code­base, using the 
contents of the doc­blocks. 
 
Of particular importance when documenting different code segments is to describe their 
significance in the larger context of the application. Having a complex­independent textual 
description of the documented object helps to optimise developer time and eases the process of 
working with sections of the application code that the developer does not have intimate 
knowledge of.  
 
For class methods, a key component of the doc­block contents is the list of arguments. These 
list the variable name, data­type and a short description of its role in the method 
implementation. Together with the description of the return value, these provide a compact way 
of documenting the methods input/output interface. In most cases, where arguments are 
primitive objects, their description would not need to be long. However, when the methods are 
designed to work with complex objects (associative arrays or generic objects), it is essential to 
use the doc­block to describe the internal structure of these variables as otherwise this hides 
the method complexity and can slow down significantly the development process using the 
method in question.  
 
**Reference:**
http://www.phpdoc.org/docs/latest/references/phpdoc/index.html 

Doc­Block Structure:   
```php
/** 
 * <­­ one line description of method goes here ­­> 
 *  
 * <­­ functional description of the method goes here ­­> 
 * 
 * @param <datatype> $varname <­­ contextual meaning of argument here ­­> 
 * ... 
 * ... 
 * @param <datatype> $varname <­­ contextual meaning of argument here ­­> 
 * 
 * @return <­­ return value datatype ­­>   
*/
public function doSomething($arg1, $arg2, ..) {
    ...
    return $value;
} 
```
#Fictional Example: 
```php
/** 
 * Method to retrieve a set of entities from the database using a search term  
 *  
 * Checks the database for entities which contain $searchTerm value in an 
 * attribute called $searchField. The ordering and formatting of result is 
 * controlled by the keys in the $params array. 
 *  
 * Structure of $params array: 
 * 
 * $params = array(  
 *     'order'    => 'asc',   // sets ordering, expecting: "asc"/"desc" 
 *     'orderBy'  => 'id',    // specifies entity field by which to order result 
 *     'format'   => 'obj',   // whether to get each entity as an object or array ('arr') 
 *     'idOnly'   => false    // whether to return the full entity data or just its id 
 * ); 
 *  
 * @param string $searchTerm  Term to compare entity attributes against 
 * @param string $searchField Name of object attribute from where to get data  
 *                            for comparison with $searchTerm. 
 * @param array  $params      Array to control the formatting and order of query  
 *                            result 
 * 
 * @returns array List of resulting entities
 */
public function findEntities($searchTerm, $searchField, $params) {
    ...
```
#Validation of method arguments 
The methods on the model classes should all verify the argument supplied to them in order to 
minimise the effects of runtime errors associated with the argument variables. This is particularly 
important in the methods that communicate with the database where implicit datatype 
conversion is likely to occur at the database server which can cause data loss or corruption. An 
example where such conversion would be particularly harmful is the manipulation of date strings 
which if invalid would not raise errors but will be converted and processed by the database 
silently. 
 
A reasonable implementation of the methods would confirm that the supplied arguments are not 
null, are of the appropriate data types and in the cases of compound variables (arrays or 
objects), they have the necessary structure for the needs of the method. In case of a problem, 
the method should raise an exception which should be caught by the controller at a higher level. 
During validation, focus should be given on simple checks that are consistent across methods in 
a way that does not significantly increase the complexity of the method code. Checks should 
prevent the raising of runtime errors, i.e. due to non­existent array key being accessed and for 
complex data members (e.g. email address, date string, etc) external validators should be used 
whenever possible. 
 
Due to the **proximity** of the models to the database itself it is important to ensure that they 
provide their own validation and handle invalid inputs robustly, regardless of any validation that 
might have been carried out in the application controllers or front end. Concentrating the 
validation in the model classes ensures that the robustness of the application can be tested in a 
well controlled environment via unit tests. Due to the close coupling of the Controller classes to 
the actual application View (HTML), unit testing for them in inherently more complex than for the 
Models. 
 
#For an example consider the beginning of a fictional class method: 
 
 ```php 
public function findEntities($searchTerm, $searchField, $params) { 
 
    // assuming no empty queries are allowed 
    if (!is_string($searchTerm) || empty($searchTerm)) { 
        // exceptions should provide reasonable/descriptive messages 
        throw new Exception('No empty queries allowed.'); 
    } 
 
    // a search query should be directed at a field 
    if (!is_string($searchField) || empty($searchField)) { 
        // exceptions should provide reasonable/descriptive messages 
        throw new Exception('No field for query specified.'); 
    } 
     // ensure that $params is an array  
    if (!is_array($params)) { 
        // exceptions should provide reasonable/descriptive messages 
        throw new Exception('Invalid $params argument supplied.'); 
    } 
 
    // ensure that $params contains appropriate keys 
    if (!array_key_exists('order', $params)) { 
        // exceptions should provide reasonable/descriptive messages 
        throw new Exception('No orderBy key supplied to $params argument.'); 
    } 
   
    ... 
```
This example can be extended to include number, object or classes arguments. In the cases 
where the argument is a string representation of an object (i.e. comma separated list of integers 
or a date string) it is preferable to use the PHP representation of those (i.e. arrays for lists and 
DateTime objects). If nevertheless, raw strings are chosen, their format should be verified 
before they are used to construct database queries. This ensures that data validation is 
performed in the controlled environment of the application and no unnecessary database 
queries are made, i.e. when the query is malformed due to invalid method arguments. 

#3.Unit Testing 
A comprehensive suite of unit tests should be created in conjunction with most application code 
that is being written. The purpose of writing those is to provide means of automatically testing 
the consistency of the existing application functionality and help in the process of identifying 
bugs earlier in the development process. Having a robust set of test cases is particularly 
important for the application model classes which handle client data and their use should help to 
reduce the instances of data corruption as a result of faulty application code. Additionally, a 
comprehensive and fully documented test suite is a great tool for learning how the application 
should work (understanding its business logic) and could be particularly useful for introducing 
new developers to the codebase. 
 
For the purpose of writing the test cases the PHPUnit testing framework should be used. The 
framework allows for the creation of test case classes that have a one­to­one correspondence 
of the application classes under testing. Unit test classes should be created as soon as a new 
class is added to the application (or even before if TDD is adhered to) and the tests should be 
updated regularly to reflect any changes that could have been made to the application code. To 
make best use of the existing test classes, the full test suite should be run before any push to or 
pull from central repository. This should ensure that changes are always made to a fully working 
application codebase. Particular attention to passing the tests should be given when code is 
merged into the central codebase so that the developer can be certain that their changes have 
not introduced problems into the application. 
 
In order to make most effective use of the tests, several key points should be considered and 
wherever possible a set of guidelines should be followed when writing test code. As the 
application models mostly do operations with information stored in the database it is essential to 
maintain a set of tools (scripts) that could generate from scratch a fully functioning testing 
database that uses the latest schema and contains all necessary entities for running of the 
tests. Any changes done to the database schema as a result of changing application 
requirements should be reflected immediately in the test database generation tools and unit 
testing code so that the testing suite is kept up to date. Reliance on a specific database state 
could be decreased by making use of temporarily added database entities which can be created 
and destroyed using the PHPUnit setUp() and tearDown() methods respectively. 
 
#Unit test guidelines: 
* Running the full unit test suite should leave the database unchanged. No extra temp 
entities should remain and no entities should be missing or be modified (as a result of 
delete or update/edit). It should be possible to run the full suite N number of times and 
get identical results each time. 
* Test methods (cases) which use any non­trivial implementation should be annotated 
using inline comments. 
* All test cases should contain appropriately formatted doc­block headers which can also 
contain detailed description of the method implementation or any notes that should be 
kept in mind by other developers. 
* Test cases should test several aspects of the method behaviour and not only consider 
the simplest test that would ensure full coverage. Suitable examples of tests that could 
be made to the methods are: 
 
     * test results on invalid input (malformed or with missing entities) 
     * test results on non existent input (empty result or exception) 
     * test results on valid input 
     * force exceptions wherever possible 
     * Whenever possible a code coverage of at least 85% percent should be aimed for. 
 
For examples of how to implement testing code that adheres to these guidelines and 
recommendations, developers could refer to the **RapidFunnel_Model_AccountUserTest** class 
which is part of the test suite on the development branch of the code repository for the 
application. 


