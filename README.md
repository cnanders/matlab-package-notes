# Working With Packages in MATLAB

MATLAB packages provides a means to organize / scope MATLAB classes and functions. Packages also enable you to reuse the names of classes and functions in different packages.  See the [MATLAB Package Documentation](https://www.mathworks.com/help/matlab/matlab_oop/scoping-classes-with-packages.html) for more information.


<a name="access"></a>
## Accessing Classes Within a Package

Consider the following project structure:
- project 
  - vendor  
    - github
      - cnanders
        - matlab-npoint
          - src
            - +npoint
              - +lc400
                - LC400.m
        - matlab-hex
          - src
            - +hex
              - HexUtils.m
  - file_a.m
  - file_b.m

Once the package has been added to the MATLAB path (see [Adding Packages to the MATLAB Path](#adding), below) there are two ways to access classes within a package. 

  1. Through the full qualified namespace, i.e., `lc400 = npoint.lc400.LC400();`
  2. Alternatively, you can import a package or class, e.g., `import npoint.lc400.LC400` within the scope of a script or function and access the class directly, e.g., `LC400`.  With this approach, you don’t have to use the full qualified name within the scope of the import.

<a name="adding"></a>
## Adding Packages to the MATLAB Path 
 
**Package folders (ones that start with the  “+” character) cannot be added to the MATLAB path.** 

Instead, you must add the parent folder of the package to the MATLAB path. 

### Example 1

To acces the `HexUtils` class from `file_a.m`,  `file_a.m` should  add the parent folder of the “+hex” package to the MATLAB path 
```
addpath('vendor/github/cnanders/matlab-hex/src')
``` 
Static methods of the `HexUtils` class could then be invoked with `hex.HexUtils.add("AF", "0C")`, for example.


### Example 2

To acces the `LC400` class from `file_a.m`,  traverse from LC400 up to the root of its package, i.e., `+npoint`.  `file_a.m` should  add the parent folder of the “+npoint” package to the MATLAB path

```
addpath('vendor/github/cnanders/matlab-npoint/src')
```
An instance of `LC400` could be created with `lc400 = npoint.lc400.LC400()`, for example.

