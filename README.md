# InterfaceActivityBuilder
Resolve Canonic Model of Interfaces and Generate Activity Code for preparing DTO objects and mapping with proxy native fields.

## Getting Started

This project intented for code generate with using command prompt like svcutil.exe. As an interface development, after creating proxy class with svcutil.exe, most of time required to write mapping codes for calling web service. This project provide that generate mapping codes automaticly.

### Usage

You can use exe file with cmd as below command in command prompt;

```
InterfaceActivityBuilder.exe 'path'
```

Example usage of exe;

```
InterfaceActivityBuilder.exe C:\Users\ezozkme\Desktop\Book2.xlsx
```

Or you can directly run exe file and pass path parameter in Console Aplication.

### Success

After running command, program executed C# file at spesific folder location which already run existing exe file. This success message writes console as below;

```
$"SUCCESS : {className}.cs successfully created in this folder location : {currentDirectory}."
```

## Requirements

Before run the program you must configure system and some assumptions should be knew.

### "AssemblyPath" Configuration Key 

Program needs to know proxy class reflection types, so before start to program you should put AssemblyPath configuration in InterfaceActivityBuilder.exe.config file.

```
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6.1" />
    </startup>
  <appSettings>
    <add key="AssemblyPath" value="C:\source\AmxOnePeruDevelopment\AMXPeruTCRM\AmxPeruCommonLibrary\bin\Debug\AmxPeruCommonLibrary.dll" />
  </appSettings>
</configuration>
```

### Excel Format

Program required one parameter which is excel file path. So this excel file should be 2 column and these column values could be below format;

```
FieldName	CANONICO

DecisionID	ConsultarRetencionEnrutamientoRequestMessage/_customerOrder/_partyOrder/ID
solicitud	ConsultarRetencionEnrutamientoRequestMessage/_solicitud
...	
```

### Attribute Canonic Names in Excel

If there is an attribute canonic names and 2 canonic name in one row at excel, the '--' seperate character should be exist. Otherwise program cant evaluate second phrase.

```
FieldName	CANONICO

origen	"ConsultarRetencionEnrutamientoRequestMessage/_solicitud/_customerOrder/_partyRole/_service/_serviceSpecification/_serviceSpecCharacteristic/_serviceSpecCharacteristicValue/value --
ConsultarRetencionEnrutamientoRequestMessage/_solicitud/_customerOrder/_partyRole/_service/_serviceSpecification/_serviceSpecCharacteristic/name (agg=""origen"")"

...	
```

### Proxy Class Namespace

The given assembly path configuration dll should be exist proxy native classes which already generated by svcutil before. So when you create proxy class your dll, the name of the namespace should be same as generated Request Type. This is main assumption of program. Afterwards this could be take from configuration file also.

```
 #region ASSUMPTIONS !!!!!
    // ASSUMPTIONS !!!!!
    // ValidarDeudaLimiteRequestMessage
    // Proxy class should be in namespace which equals to Request message parameter and remove RequestMessage part.i.e. below proxy name space is should be ValidarDeudaLimite--RequestMessage
    // public ValidarDeudaLimiteRequestType ValidarDeudaLimiteRequestMessage;
    // ASSUMPTIONS !!!!!
#endregion

...	
```

# Background of InterfaceActivityBuilder

There are 3 module to evaluate canonic messages and convert to generated c# code.

* Excel Reader - Reads the excel and makes a record for each row in cannonic list - there is a list of lines here.
* Tree Builder - It reads the line list and translates it into Tree structure, translating the canonic string into tree structure. Special cases like Attributes added 2 times in tree as expected.
* CodePad - This module iterate the Tree and recursively generate the code and do it as a file.

# Next Releases

This program only generated request part of mapping activities with proxy classes. And this program only solve spesific problem of customer requirements. So it will evolve a product and extent with new features as listed below;

* Generate DTO classes and types acording to excel input. Also need to add new type column into excel in order to generate DTO classes with correct and complex types. 
* Generate MapResponse method which provide that load to response of native proxy class to our DTO response classes.
* Refactor CodePad module in order to decrease complexity of codes for faciliate future extentions.


## Authors

* **Mehmet Ozkaya** - *Initial work* - [timetotrace](https://github.com/timetotrace)

See also the list of [contributors](https://github.com/your/project/contributors) who participated in this project.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

