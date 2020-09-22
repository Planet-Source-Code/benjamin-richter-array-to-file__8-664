<div align="center">

## array\-to\-file


</div>

### Description

Code reads an array and writes array's php code to a file.
 
### More Info
 
array_to_file($array array,$arrayname string,$filename string)

none (writes file)


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Benjamin Richter](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/benjamin-richter.md)
**Level**          |Intermediate
**User Rating**    |5.0 (10 globes from 2 users)
**Compatibility**  |PHP 4\.0
**Category**       |[Data Structures](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/data-structures__8-8.md)
**World**          |[PHP](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/php.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/benjamin-richter-array-to-file__8-664/archive/master.zip)





### Source Code

```
<?
 /* Array to File */
 function __process_array($array,$indent)
 {
 $ret_str = "";
 $first = true;
 foreach ($array as $key => $value)
 {
  if (!$first)
  $ret_str .= ",\n";
  else
  $first = false;
  $ret_str .= str_repeat(" ",$indent);
  if (is_array($value))
  {
  $ret_str .= "'$key' => array(\n".__process_array($value,$indent+5)."\n".str_repeat(" ",$indent).")";
  }
  elseif (is_string($value))
  {
  $ret_str .= "'$key' => '$value'";
  }
  elseif (is_int($value))
  {
  $ret_str .= "'$key' => $value";
  }
  elseif (is_bool($value))
  {
  $ret_str .= "'$key' => ".($value?"true":"false");
  }
 }
 return $ret_str;
 }
 function array_to_file($array,$name,$filename)
 {
 $file_str = "<?\n $"."$name = array(\n";
 $file_str .= __process_array($array,6);
 $file_str .= "\n );\n?>";
 $file = fopen($filename,"w");
 fwrite($file,$file_str);
 fclose($file);
 }
?>
```

