1. Get a list of available commands for execution 
```
terraform -help
```
2. Displays a tree of providers used in the configuration files 
```
terraform providers
```
3. to check the accuracy of the data in the directory. 
```
terraform validate
```
4.To down the code for the provided inside the Terraform configuration folder - refresh, update and prepare directories
```
terraform init 
```
5. To delivers an execution plan- sanity check of the code that shows the changes will occur during creating an infrastructure
```
terraform plan 
```
6. To generate the visual execution graph of Terraform resources
```
terraform graph
```

NOTE: The graph is outputted in DOT format. You can copy this code into the GraphViz Online viewer (https://dreampuf.github.io/GraphvizOnline/) to see the visual representation.
 - VSCODE use plugin
7. To execute/ apply the command complies with the terraform plan command.
```
terraform apply
```
 
 Note: to see the option please check with "-help" [ Example :  terraform apply -help ] 
