# Development: Get the Generator

The following is only required if you want to contribute to the development of the generator or want to use the generator locally without installing it globally from npm. If you just want to use the generator, you can install it globally from npm and skip the following steps.

Repository: <https://github.com/onecx/onecx-svc-generator>

1. Clone the **onecx-svc-generator** repository into a folder on the local machine (e.g. in wsl2)  
```bash  
git clone https://github.com/onecx/onecx-svc-generator.git  
```
2. Navigate into the cloned repository  
```bash  
cd onecx-svc-generator  
```
3. Build the Generator  
```bash  
mvn clean package -Dquarkus.package.type=uber-jar  
```
