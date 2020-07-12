# ORMFramework
A framework designed for making the database mangment facile
# Features
The TMORMFramework is designed to make the database related operations & data handling convinient. The user sends the data to the framework in object form which is than 
validated and the query is executed accordingly. Some of it's features are:
- Contains a GUI Application designed to make the beans files and required connection file easily.
- Eliminates the hassle of writing the same sql statements again and again.
- Reduces time & effort.
- Reduces the syntax error.
- Easy to switch databases and tables.
- Easy to code for sql operations.

# Installation
- Download the repository files (project) from the download section.
- Place the downloaded Files somewhere in your storage device.

# Requirements
- Well all you need is jdk-13 or heigher installed on your system.

### **The framework contains a tool to create all the below required files  in just a click although if the programmer wants to create it manually it must be done accordingly.**
- The programmer needs to create a connection file named as "connection.json" and place it in the working directory or in parallel to TMORM.jar
- Other than this the programmer needs to create a java(Bean) file which will contain the setter & getters for the fields of Table to be used.
- The Programmer needs to apply annotations accordingly over the class & methods the annotations required are below.
The **connection.json** contains following fields in json form:
- **url**
- **DBName** : the name of the databse.
- **driver** : path of required class file.
- **username** 
- **password**
**snippet shown below** :
```
{"url":"jdbc:mysql://localhost:3306/database_name","DBName":"database_name","driver":"com.mysql.jdbc.Driver","username":"username_here","password":"password_here"}
```

# Annotations
- **Table** : This annotation is to be applied over class which has field as name to which you need to provide the table name. Snippet shown below:
```
@Table(name="tableName")
```
- **View** : Just like table annotation this annotation is to applied over Class if the accesing Database is a View. It has field name to which you have to assign the View name.
```
@View(name="View_name)
```
- **Column** : The column annotation is to applied over getters to which field they represnt accordingly. you need to assign column name to name attribute of it.
```
@Column(name="columnName")
```
- **PrimaryKey** : This annotation is to applied oe=ver the getter which represnt the primary key column of the table/view.
```
@Primarykey()
```
- **ForeignKey** : The foreign key annotation is to applied over the method which represnt the foreign key column.
```
@ForeignKey()
```
- **Nullable** : This annotation is to applied over the getter which represnt the column which is nullable.
```
@Nullable()
```
- **AutoIncrement** : An annotation which is to applied over the getter representing the column which is autoIncrement.
```
@AutoIncrement()
```
**Don't worry if you mistakenly apply any of the annotation as it will all be validated.**

# GUI Usage
To use the GUI application the programmer needs to run App class from cmd. You can also just run the run.bat file from the cmd prompt provided above.
```
java -cp d:\programs\test\lib\*;d:\programs\test\classes; APP.java
```
- The application will allow you to create "connection.json" file by clicking on new button. After creating the **connection** file the Continue button will be enabled
which will redirect you to new Window.
- This window will show you list of all available tables & views on the selected database.
- The programmer needs to provide the name of class File to be created you can also see all the methods of the selected tbale/view here.
- To create the file just click on **Save** button.

# Usage
- After creating the required files you program now just need to create a java file which contains The pointer of **TMORM**. 
Following operations can be applied over the database:

#### Insert
To insert data in table the programmer need to  pass the object of bean file created for the table above to the **save** method of TMORM object. Example:

```
import com.thinking.machines.tmorm.*;
class DBBean{
  public static void main(String gg[]) throws Exception
  {
    TMORM orm=new TMORM();
    SchoolBean sb=new SchoolBean();
    //set the field values
    sb.setNumber("");
    sb.setStandard("");
    sb.setRoll_number(1311);
    sb.setBranch("");
    //execute query
    orm.save(sb);
  }
}
```

#### Update
To update data in table the programmer need to  pass the object of bean file created for the table above to the **update** method of TMORM object. Example:

```
import com.thinking.machines.tmorm.*;
class DBBean{
  public static void main(String gg[]) throws Exception
  {
    TMORM orm=new TMORM();
    SchoolBean sb=new SchoolBean();
    //set the field values
    sb.setNumber("");
    sb.setStandard("");
    sb.setRoll_number(1311);
    sb.setBranch("");
    //execute query
    orm.update(sb);
  }
}
```

#### Delete
To delete data in table the programmer need to  pass the object of bean file created for the table above to the **delete** method of TMORM object. Value for the 
primary key is to be given to delete specified record. Example:

```
import com.thinking.machines.tmorm.*;
class DBBean{
  public static void main(String gg[]) throws Exception
  {
    TMORM orm=new TMORM();
    SchoolBean sb=new SchoolBean();
    //set the field values
    sb.setRoll_number(1311);
    //execute query
    orm.update(sb);
  }
}
```

#### Select
To get data from the table programmer need to create a List of bean type representing the required table. The programmer need to call the **Select** method of TMORM which
the name of beanFile as parameter(String type).Example:

```
import com.thinking.machines.tmorm.*;
import java.util.*;
class DBBean{
  public static void main(String gg[]) throws Exception
  {
    TMORM orm=new TMORM();
    List<StudentBean> sb=new List<>();
    //will return all the records in List of object type
    sb=orm.select("StudentBean").query();
    //execute query
  }
}
```

**Need to select some specific records? Don't worry there are a bunch of methods which you can use a constraint to get the desired records.**
- **where** : The where clause can be used with methods like **equals/graterthan/lessthan** the where method takes the column_name as argument.
```
1. sb=orm.select("StudentBean").where("roll_number").eq(11).query();//equals
2. sb=orm.select("StudentBean").where("roll_number").greaterThan(555).query();//greate_than
3. sb=orm.select("StudentBean").where("roll_number").lessThan(21).query();//less_than
```
**The greaterThan & lessThan can be applied over columns with numeric datatypes**

- **Greater Than** : The greater than clause can be used with **greaterThan** method(shown above).  
- **less Than** : The less than clause can be used with **lessThan** method(shown above).  
- **OrderBy** : The OrderBy Clause can be used by calling **orderby()** method. The Method takes the column_name as argument.
The programmer need to specify the order type(ascending/descending) by calling **asc()/desc()**
method accordingly. If the user dont specify the order type than the default is ascending.
- **Limit** : The limit clause can be used by calling limit method which takes the argument of numeric type. 
