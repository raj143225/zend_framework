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

#Fictional Example: 

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
