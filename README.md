# Wrapper container

## Описание
Данный модуль нужен для внедрения зависимостей (DI).  
Внутри модуля используется пакет [di/v2](github.com/sarulabs/di/v2).
## Пример использования
``` go
package main

import (
	"log"

	"github.com/requiemofthesouls/container"
)

type Some struct {}

func New() *Some {
	return &Some{}
}

const DIWrapper = "example"

func init() {
	container.Register(func(builder *container.Builder, _ map[string]interface{}) error {
		return builder.Add(container.Def{
			Name: DIWrapper,
			Build: func(cont container.Container) (interface{}, error) {
				return New(), nil
			},
		})
	})
}

func main() {
	var (
		diContainer container.Container
		s           *Some
		err         error
	)
	if err = diContainer.Fill("container_name", &s); err != nil {
		log.Fatal(err)
	}
	
	log.Println(s)
}
```
## Пример конфигурации
У данного модуля отсутсвует конфигурация через файл.
## Зависимости от модулей
Зависимости у данного модуля отсутствуют.
