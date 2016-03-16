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
