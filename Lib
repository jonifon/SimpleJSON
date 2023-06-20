using System.Collections;
using System.Reflection;
using System.Text;

namespace bytearray.JsonLibrary
{
    public class JsonParser
    {
        public object Parse(string json)
        {
            return ParseValue(json);
        }

        private object ParseValue(string json)
        {
            if (json.StartsWith("{"))
            {
                return ParseObject(json);
            }
            else if (json.StartsWith("["))
            {
                return ParseArray(json);
            }
            else if (json.StartsWith("\""))
            {
                return ParseString(json);
            }
            else if (json == "true" || json == "false")
            {
                return bool.Parse(json);
            }
            else
            {
                return double.Parse(json);
            }
        }

        private Dictionary<string, object> ParseObject(string json)
        {
            Dictionary<string, object> result = new Dictionary<string, object>();
            string[] keyValuePairs = json.TrimStart('{').TrimEnd('}').Split(',');
            foreach (string keyValuePair in keyValuePairs)
            {
                string[] pair = keyValuePair.Split(':');
                string key = pair[0].Trim().Trim('"');
                string value = pair[1].Trim();
                result[key] = ParseValue(value);
            }
            return result;
        }

        private List<object> ParseArray(string json)
        {
            List<object> result = new List<object>();
            string[] values = json.TrimStart('[').TrimEnd(']').Split(',');
            foreach (string value in values)
            {
                result.Add(ParseValue(value));
            }
            return result;
        }

        private string ParseString(string json)
        {
            return json.Trim('"');
        }
    }

    public class JsonSerializer
    {
        public string Serialize(object obj)
        {
            StringBuilder sb = new StringBuilder();
            SerializeValue(obj, sb);
            return sb.ToString();
        }

        private void SerializeValue(object value, StringBuilder sb)
        {
            if (value == null)
            {
                sb.Append("null");
            }
            else if (value is string str)
            {
                SerializeString(str, sb);
            }
            else if (value is ICollection collection)
            {
                SerializeArray(collection, sb);
            }
            else if (value.GetType().IsClass)
            {
                SerializeObject(value, sb);
            }
            else
            {
                sb.Append(value.ToString());
            }
        }

        private void SerializeObject(object obj, StringBuilder sb)
        {
            sb.Append("{");
            PropertyInfo[] properties = obj.GetType().GetProperties();
            foreach (PropertyInfo property in properties)
            {
                if (property.CanRead)
                {
                    object value = property.GetValue(obj);
                    SerializeProperty(property.Name, value, sb);
                }
            }
            sb.Length--;
            sb.Append("}");
        }

        private void SerializeProperty(string name, object value, StringBuilder sb)
        {
            sb.Append($"\"{name}\":");
            SerializeValue(value, sb);
            sb.Append(",");
        }

        private void SerializeArray(ICollection collection, StringBuilder sb)
        {
            sb.Append("[");
            foreach (object item in collection)
            {
                SerializeValue(item, sb);
                sb.Append(",");
            }
            if (collection.Count > 0)
            {
                sb.Length--;
            }
            sb.Append("]");
        }

        private void SerializeString(string str, StringBuilder sb)
        {
            sb.Append($"\"{str.Replace("\\", "\\\\").Replace("\"", "\\\"")}\"");
        }
    }
}
