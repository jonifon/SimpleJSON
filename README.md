# SimpleJSON
Простая библиотека для работы с JSON на C#, преимущественно для чтения JSON данных.

# **Как использовать**

## **JsonParse**
JsonParser предоставляет возможность парсить JSON строку и возвращать объект C#.

### **Методы**

**object Parse(string json)**

Метод принимает JSON строку и возвращает объект, соответствующий этой строке.

### **Пример использования**
```
string jsonString = "{\"name\":\"Илья\",\"age\":50,\"city\":\"Москва\"}";
JsonParser parser = new JsonParser();
Dictionary<string, object> jsonObject = (Dictionary<string, object>)parser.Parse(jsonString);

Console.WriteLine("Имя: {0}", jsonObject["name"]);
Console.WriteLine("Возвраст: {0}", jsonObject["age"]);
Console.WriteLine("Город: {0}", jsonObject["city"]);
```

Результат:
```
Имя: Илья
Возвраст: 50
Город: Москва
```

## **JsonSerializer**
JsonSerializer предоставляет возможность сериализовать объект C# в JSON строку.

### **Методы**

**string Serialize(object obj)**
Метод принимает объект и возвращает его в виде JSON строки.

### **Пример использования**
```
 MyObject obj = new MyObject()
 {
     Name = "Илья",
     Age = 50,
     City = "Москва"
 };
 JsonSerializer serializer = new JsonSerializer();
 string jsonString = serializer.Serialize(obj);
 Console.WriteLine(jsonString);
```

Результат:
```
{"Name":"Илья","Age":50,"City":"Москва"}
```
