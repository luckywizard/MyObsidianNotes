
### 一、快速入门
#### 1. 打开几何文件
- To open the first tutorial file (see Appendix A [Tutorial], page 127), select the ‘File->Open’  
menu, and choose t1.geo

#### 2. 生成网格
- To perform the mesh generation, go to the mesh module   
>[!note]
>by selecting ‘Mesh’ in the tree:
>and  choose the dimension (‘1D’ will mesh all the curves; ‘2D’ will mesh all the surfaces—as well as  all the curves if ‘1D’ was not called before; ‘3D’ will mesh all the volumes—and all the surfaces  if ‘2D’ was not called before).
- To save the resulting mesh in the current mesh format click on  **‘Save’,** or select the appropriate format and file name with the ‘File->Export’ menu.

#### 3. 添加几何元素
- To create a new geometry or to modify an existing geometry, select ’**Geometry**’ in the tree.
>[!note]-
> For  example, to create a spline, select ‘Elementary entities’, ‘Add’, ‘New’ and ‘Spline’. You will then  be asked to select a list of points, and to __type e to finish the selection (or q to abort it)__. Once  the interactive command is completed, a text string is automatically added at the end of the  current script file.


### 二、数据结构相关

#### 1. 模型实体创建
实体可以以“自下而上”的方式（首先是点，然后是曲线、曲面和体积）或以“构造实体几何”方式（在其上执行布尔运算的实体）构建。这两种方法也可以结合使用。最后，可以基于基本几何实体定义模型实体组（称为“物理组”）。
>[!note]-
>The entities can either be built in a “bottom-up” manner (first points, then curves, surfaces and volumes) or in a “Constructive Solid Geometry” fashion (solids on which boolean operations are performed). Both methodologies can also be combined. Finally, groups of model entities (called “physical groups”) can be defined, based on the elementary geometric entities.

>[!note] Geometry: model entity creation
>A model in Gmsh is defined using its Boundary Representation (BRep): a volume is bounded by a set of surfaces, a surface is bounded by a series of curves, and a curve is bounded by two end points. 
>Model entities are topological entities, i.e., they only deal with adjacencies in the model, and are implemented as a set of abstract topological classes. This BRep is extended by the definition of embedded, or internal, model entities: internal points, edges and surfaces can be embedded in volumes; and internal points and curves can be embedded in surfaces.
>

#### 2. 有限元网格生成
网格生成是自下而上的：首先对曲线进行离散化；然后使用曲线的网格对曲面进行网格划分；然后使用曲面的网格对体积进行网格划分。在此过程中，实体的网格仅受其边界网格的约束，除非较低维度的实体明确嵌入到较高维度的实体中。
>[!note]-
> In order to guarantee the conformity of the mesh, mesh generation is performed in a bottom-up flow: curves are discretized first; the mesh of the curves is then used to mesh the surfaces; then the mesh of the surfaces is used to mesh the volumes. In this process, the mesh of an entity is only constrained by the mesh of its boundary, unless entities of lower dimensions are explicitly embedded in entities of higher dimension.


### 三、语法

![[Pasted image 20220729090613.png]]




### 四、语法

##### 1.当 ~{expression} 附加到字符串字符串时，结果是由字符串、_（下划线）和表达式的值连接形成的新字符串.
>[!note]-
>When ~{expression} is appended to a string string, the result is a new string formed by the concatenation of string, _ (an underscore) and the value of the expression
```gmsh
For i In {1:3}
	x~{i} = i; 
EndFor 
is the same as 
	x_1 = 1;
	x_2 = 2; 
	x_3 = 3; 
```

##### 2. 方括号 [] 允许从列表中提取一项（也可以使用圆括号代替方括号）。
>[!note]-
>The brackets [] permit to extract one item from a list (parentheses can also be used instead of brackets). 

##### 3.Find 搜索
>[!note]-
>1. Find searches for occurrences of the first expression in the second (both of which can be lists). 
>2. StrFind searches the first char-expression for any occurrence of the second char-expression. 

##### 4. StrCmp 比较两个字符串
>[!note]-
> StrCmp compares the two strings (returns an integer greater than, equal to, or less than 0, according as the first string is greater than, equal to, or less than the second string). StrLen returns the length of the string. 

##### 5.属性
>[!note]-
> TextAttributes creates attributes for text strings. 
>. Exists checks if a variable with the given name exists (i.e., has been defined previously), and 
>. FileExists checks if the file with the given name exists. 
>. StringToName creates a name from the provided string. GetNumber allows to get the value of a ONELAB variable (the optional second argument is the default value returned if the variable does not exist). 
>. GetValue allows to ask the user for a value interactively (the second argument is the value returned in non-interactive mode). For example, inserting GetValue("Value of parameter alpha?", 5.76) in an input file will query the user for the value of a certain parameter alpha, assuming the default value is 5.76. If the option General.NoPopup is set (see Section B.1 [General options list], page 173), no question is asked and the default value is automatically used. 

### 五、几何模型

###### 1. Geometry module
这些几何模型实体在 Gmsh 中也被称为“基本实体”，并在创建时被分配标签（**严格为正的全局标识号**）： 
- 1. 每个点必须拥有唯一的标签； 
- 2. 每条曲线必须拥有唯一的标签； 
- 3. 每个表面必须具有唯一的标签； 
- 4. 每卷必须有一个唯一的标签。
然后可以以各种方式操纵基本实体，例如使用**平移、旋转、缩放或对称**命令。可以使用 Delete 命令删除它们，前提是没有更高维度的实体引用它们。系统为特殊用途保留零标签或负标签：不要在脚本中使用它们。


###### 2. Points
创建一个点。括号内的表达式是点的标签；右侧大括号内的三个第一个表达式给出了三维欧几里得空间中点的三个 X、Y 和 Z 坐标；可选的最后一个表达式在该点设置规定的网格单元大小。
>[!note]-
>- Point ( expression ) = { expression, expression, expression <, expression > }; 
>
>Create a point. The expression inside the parentheses is the point’s tag; the three first expressions inside the braces on the right hand side give the three X, Y and Z coordinates of the point in the three-dimensional Euclidean space; the optional last expression sets the prescribed mesh element size at that point. 


3. Curves
创建一条直线段。括号内的表达式是线段的标签；右侧大括号内的两个表达式给出了段的起点和终点的标签。
>[!note]-
>- Line ( expression ) = { expression, expression }; 
>
>Create a straight line segment. The expression inside the parentheses is the line segment’s tag; the two expressions inside the braces on the right hand side give tags of the start and end points of the segment. 




4. 
