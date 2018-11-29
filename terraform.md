# Terraform


```terraform init``` - downloads the used providers from the hashicorp

```terraform plan``` - difference between the local and remote configuration

```terraform apply``` - apply the local configuration to remote platform

```terraform destroy``` - destroy all resources defined in the local configuration. Not recommended to use it in production

```terraform validate``` - validate the definition of the resource files/parsing issues

```terraform fmt``` - formats the resource files

```terraform state show <resource name>```

```terraform graph``` - dependency on GraphViz
```
terraform graph | dot - Tsvg > graph.svg # generates a SVG grahical file
```

```terraform workspace```
```
terraform workspace new <workspace name> ...logically separates the local project
terraform workspace list
terraform workspace select <name>
terraform workspace delete <name>
```

```terraform output``` - pull the value of assigned value to a variable

```terraform import``` - imports the existing state

```terraform refesh``` - 

```terraform taint <resource_name>``` - recreates a defined resource. immutable style. 
then execute ```terraform apply```

```terraform untain <resource_name>``` - remove the resource from the "recreate"

## VARIABLES:
3 types: string, map, listtype

### string
```

variable "newvar" {
  type = "string"
  default = "value"
}
```

### map

```
variable "maptype" {
type = "map"
  default = {
   subnet1 = "subnet1"
   subnet2 = "subnet2"
  }
}
```

### list

```
variable "listtype" {
  type = "list"
  default = ["item1", "item2"]
}
```

.tfvars - file containing the variables

```"${var.var_name}"``` - placeholder of the var_name variable in the resource file
```"${var.var_list["item1"]}"``` - placeholder of the var_list

### Output variables
are show when the "apply" command is run or command "output var_name"

useful to see the calculated value during the execution
```
output "first_output" {
  value = "my fisrst output variable"
}
```


### Input variables

you are prompted to enter their values during the execution
```buildoutcfg
variable variable_name {
}
# - there is no "default" defined in the variable_name i.e. you will be promted to enter the value during the execution
# this works only with the string datatype
```

- input of the map
```
variable newmap {
  type = "map"
}
# then you pass the value with the terraform command.
terraform apply -var 'newmap={ subnet1="saly", subnet2="frank"}
```
another option is to use .tfvars file

```terraform apply -var-file="anotherfile.tfvars"```

### Syntax interpolation
https://www.terraform.io/docs/configuration/interpolation.html

#### Useful functions
- ```cidrsubnet(iprange, newbits, netnum)``` - Takes an IP address range in CIDR notation (like 10.0.0.0/8) and extends its prefix to include an additional subnet number. For example, cidrsubnet("10.0.0.0/8", 8, 2) returns 10.2.0.0/16; cidrsubnet("2607:f298:6051:516c::/64", 8, 2) returns 2607:f298:6051:516c:200::/72.


### Side notes

- special file ```terraform.tfvars``` - the values of the variables in this file are used during the complicaiton of the terraform resources. E.g. when you execute ```terraform validate```.

- you can write a simple bash script to execute the terraform with addition parameters (e.g. with ```-var-files=""```)

- use ```description```for the variables - it may help others and you too

- variables can be also passed to terraform from environment variables, when they are prefixed with ```TF_VAR_```

### Debugging

- set env variable ```TF_LOG=TRACE``` for the most verbose logs. Other values are ```DEBUG, INFO, WARN, ERROR```

