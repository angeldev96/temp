
# Pasos para implementar el logica de exportar tablas a pdf 

1. Instalar TextSharp.LGPLv2.Core con Nuget
2. Copiar las dependencias en los .aspx.cs donde ira la implementacion.

```
using iTextSharp.text;
using iTextSharp.text.pdf;
using System.IO;
```
3. Funcion del boton de exportar a pdf:

```cs
protected void btnExportPDF_Click(object sender, EventArgs e)
{
    // Configurar la conexión a la base de datos
    string connectionString = ConfigurationManager.ConnectionStrings["conexion"].ConnectionString;
    using (SqlConnection connection = new SqlConnection(connectionString))
    {
        // Consulta SQL para obtener los datos
        string query = "SELECT id, nombre, edad, ciudad, direccion, genero, estado_civil, nivel_educativo, ocupacion, ingreso_mensual FROM Beneficiario";

        // Crear el comando y asignar la conexión y la consulta
        using (SqlCommand command = new SqlCommand(query, connection))
        {
            // Abrir la conexión
            connection.Open();

            // Ejecutar la consulta y obtener los datos en un SqlDataReader
            using (SqlDataReader reader = command.ExecuteReader())
            {
                // Crear el documento PDF
                Document document = new Document();
                MemoryStream memoryStream = new MemoryStream();
                PdfWriter writer = PdfWriter.GetInstance(document, memoryStream);
                document.Open();

                // Crear una tabla con el mismo número de columnas que la GridView
                PdfPTable table = new PdfPTable(reader.FieldCount);

                // Configurar el tamaño de fuente y estilo para los encabezados de columna
                Font headerFont = FontFactory.GetFont(FontFactory.HELVETICA_BOLD, 10);

                // Agregar las cabeceras de las columnas
                for (int i = 0; i < reader.FieldCount; i++)
                {
                    PdfPCell headerCell = new PdfPCell(new Phrase(reader.GetName(i), headerFont));
                    table.AddCell(headerCell);
                }

                // Configurar el tamaño de fuente para los datos de la tabla
                Font dataFont = FontFactory.GetFont(FontFactory.HELVETICA, 8);

                // Agregar los datos de las filas
                while (reader.Read())
                {
                    for (int i = 0; i < reader.FieldCount; i++)
                    {
                        PdfPCell dataCell = new PdfPCell(new Phrase(reader.GetValue(i).ToString(), dataFont));
                        table.AddCell(dataCell);
                    }
                }

                // Agregar la tabla al documento
                document.Add(table);

                // Cerrar el documento
                document.Close();

                // Descargar el archivo PDF
                Response.ContentType = "application/pdf";
                Response.AppendHeader("Content-Disposition", "attachment; filename=datos.pdf");
                Response.BinaryWrite(memoryStream.ToArray());
                Response.End();
            }
        }
    }
}
```

4. Modificar la consulta de SQL segun la tabla a exportar

5. Agregar boton para exportar a pdf en los archivos .aspx correspondientes.

 ``` 
 <asp:Button ID="btnExportPDF" CssClass="btn btn-secondary mb-2 mx-1" runat="server" 
   Text="Exportar a PDF" OnClick="btnExportPDF_Click" />
```


