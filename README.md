# Programming Guidelines <span align="end" style="font-size: .25em;">v1.0</span>

This programming guideline contains standard conventions that are/will be used during the lifespan of this project. The goal is to produce high quality applications which has the same coding conventions and coding style. Examples that are placed in this language is in Typescript language, however most of the rules can be used in any language and some of the rules are only for object-oriented programming languages. Therefore please use this guideline as part of your development process.

Some of the common code style conventions are not included in this document (e.g. indentation or max. number of line in file), because current Integrated development environments(IDE) already provide features that handles just that.

## 1. Programming Principles

### Class Design

1. **The Single Responsibility Principle** : A class should have one, and only one, reason to change.

2. **The Open Closed Principle** : You should be able to extend a class's behaviour, without modifying it.

3. **The Liskov Substitution Principle** : Functions that use pointers or references to base classes must be able to use objects of derived classes without knowing it.

4. **The Interface Segregation Principle** : Make fine-grained interfaces that are client specific, meaning no client should be forced to depend on methods it does not use.

5. **The Dependency Inversion Principle** : Depend on abstractions, not on concretions.

### Package Cohesion

1. **The Release Reuse Equivalency Principle** : The package must be created with reusable classes — “Either all the classes inside the package are reusable, or none of them are.

2. **The Common Closure Principle** : Classes that change together are packaged together.

3. **The Common Reuse Principle** : Classes that are used together are packaged together.

### Package Coupling

Packages can be decoupled by separating their responsibility, and they can be turned into the releasable packages such as simple software libraries (e.g. DLLs).

1. **The Acyclic Dependencies Principle** : The dependency graph of packages must have no cycles, meaning each component that is can be separated from the rest of the system, it should be developed and built separately.

2. **The Stable Dependencies Principle** : Depend on the direction of stability. A package should only depend upon packages that are more stable than it is.

3. **The Stable Abstractions Principle** : Abstractness increases with stability.

#### Please refer to the following articles by Robert C. Martin for an in depth understanding:

- [The Principles of OOD][ref-1]
- [The Clean Code Blog][ref-2]

## 2. Code Style

### Naming Conventions

1. All names should be written in English names.

2. Use searchable names.

3. Don’t be cute.

        execute(); 	// NOT: doIt(); 
        abort(); 	// NOT: goodbye();


4. Names representing packages should be in all lower case.

        mypackage, com.rubikans.app.ui

5. Names representing types must be nouns and written in mixed case starting with upper case.

        Rectangle, Shape

6. Variable names must be in mixed case starting with lower case.

   	    rectangle, shape

7. Names representing constants (final variables) must be all uppercase using underscore to separate words.

        MAX_VALUE, API_PREFIX

8. Names representing methods must be verbs and written in mixed case starting with lower case.

        getName(), computeTotalWidth()

9. Abbreviations and acronyms should not be uppercase when used as name.

        exportHtmlSource(); // NOT: exportHTMLSource();
        openPdfFile();    // NOT: openPDFFile();


10. Generic variables should have the same name as their type.

        void setTopic(Topic topic); 
        
        // NOT: void setTopic(Topic value);
        // NOT: void setTopic(Topic aTopic);
        // NOT: void setTopic(Topic t);

        void connect(Database database);
        // NOT: void connect(Database db);
        // NOT: void connect(Database oracleDB)

        Furthermore, to avoid name confusion of class variable and method variable argument, variables can have prefix (e.g. new).

        void setTopic(Topic newTopic);

11. The name of the object is implicit, and should be avoided in a method name.

        employee.getName();   // NOT: employee.getEmployeeName();


12. The terms *get/set* must be used where an attribute is accessed directly.

        employee.getName();
        employee.setName(name);

        matrix.getElement(2, 4);
        matrix.setElement(2, 4, value);

13. *is* prefix should be used for boolean variables and methods.

        isSet, isVisible, isFinished, isFound, isOpen

14. *can* & *has* prefix should be used for boolean probabilities.

        canExpandBar, canViewDetails, hasContextMenu, hasModal

15. Plural form should be used on names representing a collection of objects.

        Collection<Point>  points;
        int[]              values;

15. Complement names must be used for complement entities.

        get/set, add/remove, create/destroy, 
        start/stop, insert/delete,
        increment/decrement, old/new, begin/end, 
        first/last, up/down, min/max,
        next/previous, old/new, open/close, 
        show/hide, suspend/resume, etc.

16. Abbreviations in names should be avoided.

        computeAverage();               // NOT: compAvg();
        ActionEvent event;             	// NOT: ActionEvent e;


17. Negated boolean variable names must be avoided.

        bool isError; // NOT: isNoError
        bool isFound; // NOT: isNotFound

18. Associated constants (final variables) should be in a separate class.

    	public class Color {
        	static final int COLOR_RED   = 1;
        	static final int COLOR_GREEN = 2;
        	static final int COLOR_BLUE  = 3;
    }

    or

    	public enum Color {
        	RED, GREEN, BLUE
        }

### Programming Practice Conventions

1. Numerical constants (literals) should not be coded directly, except for -1, 0, and 1, which can appear in a for loop as counter values.

        1000 * 60 * 60 * 24; 	// AVOID 
        // should be
        static final int MILLISECOND = 1;
        static final int SECOND = MILLISECOND * 1000;
        static final int MINUTE = SECOND * 60;
        static final int HOUR = MINUTE * 60;
        static final int DAY = HOUR * 24;

## 3. Code Comment

1. Comments do not make up for bad code.

2. Explain yourself in code.

        // Check to see if the employee is eligible for full benefits 
        if ((employee.flags & HOURLY_FLAG) &&
        (employee.age > 65))
        
        Or

        if (employee.isEligibleForFullBenefits())

3. Clarify obscure argument or return value into much more readable format.

        public void testCompareTo() throws Exception {
           …
           assertTrue(a.compareTo(a) == 0);  	// a == a 
           assertTrue(a.compareTo(b) != 0);  	// a != b
           assertTrue(ab.compareTo(ab) == 0); 	// ab == ab
           assertTrue(a.compareTo(b) == -1); 	// a < b
           assertTrue(aa.compareTo(ab) == -1); // aa < ab
           assertTrue(ba.compareTo(bb) == -1); // ba < bb
           assertTrue(b.compareTo(a) == 1);  	// b > a
           assertTrue(ab.compareTo(aa) == 1); 	// ab > aa 
           assertTrue(bb.compareTo(ba) == 1); 	// bb > ba
           …
        }

4. Do not add noise comments

        /** The day of the month. */
        private int dayOfMonth;

        /**
        * Returns the day of the month. *
        * @return the day of the month. */
        public int getDayOfMonth() { 
        	return dayOfMonth;
        }

5. Add *TODO*, *TODO::FIX*, *TODO::REFACTOR*, *TODO::REVIEW* comments for the job that should be done, but for some reason do not have time to do it.

6. Do not express your emotions in comment, talk to your supervisor :o

        try {
          response.add(ErrorResponder.makeExceptionString(e));
          response.closeAll(); 
        }
        catch(Exception exception) 
        {
   		//Give me a break!
        }

7. Follow comment conventions. Depending on language you are using, follow common comment conventions.

        /**
         * Return lateral location of the specified position.
         * If the position is unset, NaN is returned.
         *
         * @param x    X coordinate of position.
         * @param y    Y coordinate of position.
         * @return     Lateral location.
         * @throws IllegalArgumentException  If zone is <= 0.
         */
        public double computeLocation(double x, double y)
          throws IllegalArgumentException
        {
          ...
        }

    Many programming languages do use same comment style, however for details you can refer to Java Code Conventions, for Python please refer to Python-PEP-257-Docstring Conventions.

## 4. Testing

1. Test code must follow the same code conventions and programming styles.

2. Unit tests should be fully automated and non-interactive

3. Tests should be independent of each other.

4. Tests should be repeatable.

5. Fix failing tests immediately and do not commit/push your code to the repository if your test is failing.

6. The person who broke the test sis responsible to fix the test without deleting the test.

## 5. API Principles

### API Design

1. **Resilience** : APIs should be hosted independently on its own subdomain. This is to avoid security risks that may target a hosted to not affect the API such as blacklisting.


2. **Data Contracts** : APIs should be versioned to avoid breakage and allow for extensibility. 

   - Breaking Changes :
     - Changing a property name (e.g. from name to productName) or data type on a property (e.g. from an integer to a float).
     - Adding a required field on the request (e.g. a new required header or property in a request body).
     - Removing a property on the response (e.g. removing description from a product).

   - API Change Management :
     - Continue support for existing properties/endpoints.
     - Add new properties/endpoints rather than changing existing ones.
     - Thoughtfully sunset obsolete properties/endpoints.
     
            {
                "data": {
                "id": 1,
                "name": "Carlos Ray Norris",     // original property from v1
                "firstName": "Carlos",           // new property in v2
                "lastName": "Norris",            // new property in v2
                "alias": "Chuck",                // obsolete property in v1
                "aliases": ["Chuck", "Walker"]   // new property in v3 
            }

3. API endpoints should be nested relatively.

        https://api.rubikans.com/v1/product/stats             // NOT: https://api.rubikans.com/v1/product_stats

4. Use scoped API endpoints. An API endpoint should only affect a single resource.

    For example, when a user logs in, the API should not respond with a compound entities.

        { 
            name: "Shady"
            email: "shady@rubikans.com"
            mobile: "01234567890"
            permissions: [...permissions]
        }

    Entities should be seperated into its own endpoints.

        {
            name: "Shady"
            email: "shady@rubikans.com"
            mobile: "01234567890"
        }

        {
            permissions: [...permissions]
        }

5. Use nominative API names. API endpoints should be described with nouns.

        https://api.rubikans.com/v1/product/22/                 // NOT: https://api.rubikans.com/v1/product/get?id=22 

6. Use HTTP methods to describe functionality.

        GET::https://api.rubikans.com/v1/product/22             // NOT: https://api.rubikans.com/v1/product/22/get
        POST::https://api.rubikans.com/v1/product/              // NOT: https://api.rubikans.com/v1/product/create

    | Method | Description                                      |
    |--------|--------------------------------------------------|
    | GET    | Used to retrieve a representation of a resources |
    | POST   | Used to create new resources and sub-resource    | 
    | PUT    | Used to update existing resource                 | 
    | PATCH  | Used to update parts of an existing resource     |
    | DELETE | Used to delete existing resource                 |

7. An API should be generic, abstract and uniform. An API should not differentiate between clients but may expose endpoints that are specific to a certain client. An API should also use uniform entity models in both request and response. 


8. API response should be uniform in all endpoints regardless.

    - **2xx** :

    | Field   | Description                        | Type            |                                   
    |---------|------------------------------------|-----------------|
    | data    | Contains the requested data        | Object \| Array |
    | payload | Contains any required dependencies | Object          |

        {
            data: [...items]
            payload: {
                filters: {
                    category: [...categories]
                }
                pagination: {...meta}
            }
        }

   - **4xx - 5xx** :

    | Field   | Description                         | Type   |                                   
    |---------|-------------------------------------|--------|
    | message | Contains a description of the error | string |


9. An API should respond with the appropriate API status code. Refer to the [MDN Web Docs][ref-3] for more details.

[ref-1]:http://butunclebob.com/ArticleS.UncleBob.PrinciplesOfOod

[ref-2]:https://blog.cleancoder.com/uncle-bob/2020/10/18/Solid-Relevance.html

[ref-3]:https://developer.mozilla.org/en-US/docs/Web/HTTP/Status#information_responses