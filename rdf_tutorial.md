RDF
=============
* statement:
	* Resource
	* Property
	* Property value
* [W3C's RDF Validation Service](http://www.w3.org/RDF/Validator/)
* RDF Main Elements
	* <rdf:RDF>
		* the root element of an RDF document
		* defines the xml document to be an RDF document
		* contains a reference to the RDF namespace

	```html
	<?xml version="1.0"?>

	<RDF>
	  <Description about="http://www.w3schools.com/rdf">
		<author>Jan Egil Refsnes</author>
		<homepage>http://www.w3schools.com</homepage>
	  </Description>
	</RDF>
	```

	* 3 different methods dealing with properties (前两者经验证结果相同):
		* Defined as elements

		```html
		<?xml version="1.0"?>

		<rdf:RDF
		xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
		xmlns:cd="http://www.recshop.fake/cd#">

		<rdf:Description
		rdf:about="http://www.recshop.fake/cd/Empire Burlesque">
		  <cd:artist>Bob Dylan</cd:artist>
		  <cd:country>USA</cd:country>
		  <cd:company>Columbia</cd:company>
		  <cd:price>10.90</cd:price>
		  <cd:year>1985</cd:year>
		</rdf:Description>

		</rdf:RDF>
		```
		* Defined as attributes (必须加上引号)
		
		```html
		<?xml version="1.0"?>

		<rdf:RDF
		xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
		xmlns:cd="http://www.recshop.fake/cd#">

		<rdf:Description
		rdf:about="http://www.recshop.fake/cd/Empire Burlesque"
		  cd:artist = "Bob Dylan"
		  cd:country = "USA"
		  cd:company = "Columbia"
		  cd:price = "10.90"
		  cd:year = "1985" />

		</rdf:RDF>
		```
		* Defined as resources
		
		```html
		<?xml version="1.0"?>

		<rdf:RDF
		xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
		xmlns:cd="http://www.recshop.fake/cd#">

		<rdf:Description
		rdf:about="http://www.recshop.fake/cd/Empire Burlesque">
		  <cd:artist rdf:resource="http://www.recshop.fake/cd/dylan" />
		  ...
		  ...
		</rdf:Description>

		</rdf:RDF>
		```
* RDF Container Elements
	* Used to describe group of things
		* A container is a resource that contain things
		* The contained things are called members (not list of values)
	* 下面的表格对应着RDF，注意到这里的genid是自动生成的
	* rdf:Bag
		* Describe a list of values that do not have to be in a specific order
		* Allowed to contain duplicate values
	* rdf:Seq
		* Describe an ordered list of values
		* Allowed to contain duplicate values
	* rdf:Alt
		* Describe a list of alternative values

	```html
	<?xml version="1.0"?>

	<rdf:RDF
	xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	xmlns:cd="http://www.recshop.fake/cd#">

	<rdf:Description
	rdf:about="http://www.recshop.fake/cd/Beatles">
	  <cd:artist>
		<rdf:Bag>
		  <rdf:li>John</rdf:li>
		  <rdf:li>Paul</rdf:li>
		  <rdf:li>George</rdf:li>
		  <rdf:li>Ringo</rdf:li>
		</rdf:Bag>
	  </cd:artist>
	</rdf:Description>

	</rdf:RDF>
	```
	
	```table
	|Number | Subject | Predicate | Object
	| ---- |: ---- |: ---- 
	|1 | genid:A179883 | http://www.w3.org/1999/02/22-rdf-syntax-ns#type | http://www.w3.org/1999/02/22-rdf-syntax-ns#Bag
	|2 | http://www.recshop.fake/cd/Beatles | http://www.recshop.fake/cd#artist | genid:A179883
	|3 | genid:A179883 | http://www.w3.org/1999/02/22-rdf-syntax-ns#_1 | "John"
	|4 | genid:A179883 | http://www.w3.org/1999/02/22-rdf-syntax-ns#_2 | "Paul"
	|5 | genid:A179883 | http://www.w3.org/1999/02/22-rdf-syntax-ns#_3 | "George"
	|6 | genid:A179883 | http://www.w3.org/1999/02/22-rdf-syntax-ns#_4 | "Ringo"
	```



* RDF Collections
	* rdf:parseType="Collection"
	* A container指明了some members，可并没有拒绝other members加入其中，可a collection指明了一个群体__有且只能有__指定的members.
	
* RDF Schema (RDFS)	
	* Classes in RDF Schema are much like classes in object oriented programming languages. This allows resources to be defined as instances of classes, and subclasses of classes.
	
	```html
	<?xml version="1.0"?>

	<rdf:RDF
	xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	xmlns:rdfs="http://www.w3.org/2000/01/rdf-schema#"
	xml:base="http://www.animals.fake/animals#">

	<rdf:Description rdf:ID="animal">
	  <rdf:type rdf:resource="http://www.w3.org/2000/01/rdf-schema#Class"/>
	</rdf:Description>

	<rdf:Description rdf:ID="horse">
	  <rdf:type rdf:resource="http://www.w3.org/2000/01/rdf-schema#Class"/>
	  <rdfs:subClassOf rdf:resource="#animal"/>
	</rdf:Description>

	</rdf:RDF>
	```
	
	```html
	<?xml version="1.0"?>

	<rdf:RDF
	xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	xmlns:rdfs="http://www.w3.org/2000/01/rdf-schema#"
	xml:base="http://www.animals.fake/animals#">

	<rdfs:Class rdf:ID="animal" />

	<rdfs:Class rdf:ID="horse">
	  <rdfs:subClassOf rdf:resource="#animal"/>
	</rdfs:Class>

	</rdf:RDF>
	```
* [RDFS/RDF Classes/Properties/Attributes](http://www.w3schools.com/rdf/rdf_reference.asp)
* OWL is Different from RDF
	* OWL is a stronger language with machine interpretability 
	* OWL comes with a larger vocabulary and stronger syntax than RDF.
	* has 3 sublanguages:
		* OWL Lite
		* OWL DL
		* OWL Full
