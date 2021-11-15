# goconfig
Library for loading configuration files (yaml, ...) into structs


## Basic usage

Assuming you have a file called config.yaml in the default path 


```yaml
name: Hello
```

And a struct 
```golang
type Configuration struct {
	Name string `yaml:"name"`
}
```

Load the yaml file into the struct

```golang
    cfg := &Configuration{}
    err := NewConfigLoader().LoadConfig( c)
    name := cfg.Name
    ...
```

## Basic usage with env variables

Assuming you have a file called config.yaml in the default path
and an exported environment variable MY_PWD = "secretvalue"


```yaml
name: Hello
pwd: "{Env:MY_PWD}
```

And a struct
```golang
type Configuration struct {
	Name string `yaml:"name"`
	Pwd string  `yaml:"pwd"`
}
```

Load the yaml file into the struct

```golang
    cfg := &Configuration{}
    err := NewConfigLoader().LoadConfig( c)
    name := cfg.Name
    pwd := cfg.Pwd
    ...
```


### Different paths 

The default paths for searching a config file are
```
"", "k8s/dev/", "config/", "./config/", "/config/"
```

You can set the paths to new locations with:


```golang
    cfg := &Configuration{}
    err := NewConfigLoader().Paths("/mypath/").LoadConfig( c)
    name := cfg.Name
    pwd := cfg.Pwd
    ...
```

### Different filename

The default filename for searching is 
```
config.yaml
```

You can set the filename with:

```golang
    cfg := &Configuration{}
    err := NewConfigLoader().File("myownconfigfile.yml").LoadConfig( c)
    name := cfg.Name
    pwd := cfg.Pwd
    ...
```
