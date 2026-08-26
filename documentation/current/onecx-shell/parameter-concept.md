# Concept for Microfrontend Parameter

1. The Shell requests the parameters from the ShellBFF by product names and application ids of all applications which are part of the current workspace configuration.
2. The ShellBFF retrieves the parameters from the ParameterSVC for all applications which are part of the current workspace.
3. The ParameterSVC returns the parameters to the ShellBFF.
4. The ShellBFF sends the parameters, back to the Shell.
5. The Shell caches the parameters only if the fetch status indicates success.

Since the ShellBFF is always returning status code 200 when requested for parameters, the response structure implies if the fetching of parameters was successfull or not.

If the response object matches the request object (i.e., all products and applications are included in the response), then the fetch was successful. If there is an issue with the ParameterSVC, the response object will be empty and will not contain any products or applications.

```mermaid
 sequenceDiagram
     Shell->>+ShellBFF: getParameters (body: GetParameterRequest)
     ShellBFF->>-ParameterSVC: get parameters
     ParameterSVC-->>+ShellBFF: parameters
     ShellBFF-->>Shell: return parameters (body: GetParameterResponse)
     Note over Shell: Cache
```
