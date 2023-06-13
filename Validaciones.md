### 1. Campo que debe ser únicamente texto
Para asegurarnos de que el usuario ingrese solamente letras en un campo (sin números ni caracteres especiales), podemos usar un combinación de `RegularExpressionValidator` y `RequiredFieldValidator` en ASP.NET. Aquí te dejo un ejemplo:

```html
<div class="col-md-6 mb-3">  
	<label for="exampleInputDireccion">Nombre del alumno</label>  			
	<asp:TextBox ID="txtnombreAlum" CssClass="form-control" runat="server" autocomplete="off" Text=""></asp:TextBox>
	<asp:RequiredFieldValidator ID="rfvNombreAlum" runat="server" ControlToValidate="txtnombreAlum" ErrorMessage="Campo obligatorio" ForeColor="Red"></asp:RequiredFieldValidator> 
	<asp:RegularExpressionValidator ID="regexNombreAlum" runat="server" ControlToValidate="txtnombreAlum" ErrorMessage="Solo se permiten letras en el campo Nombre del alumno" ValidationExpression="^[a-zA-Z\s]+$" ForeColor="Red"></asp:RegularExpressionValidator>  
</div>```

Por favor, ten en cuenta que el ID del `TextBox` debe coincidir con el de `RegularExpressionValidator` y `RequiredFieldValidator`. Esto es necesario para que estos validadores sepan a qué `TextBox` están vinculados.
