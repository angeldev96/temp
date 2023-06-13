### 1. Campo que debe ser únicamente texto
Para asegurarnos de que el usuario ingrese solamente letras en un campo (sin números ni caracteres especiales), podemos usar un combinación de `RegularExpressionValidator` y `RequiredFieldValidator` en ASP.NET. Aquí te dejo un ejemplo:

```html
<div class="col-md-6 mb-3">  
	<label for="exampleInputDireccion">Nombre del alumno</label>  			
	<asp:TextBox ID="txtnombreAlum" CssClass="form-control" runat="server" autocomplete="off" Text=""></asp:TextBox>
	<asp:RequiredFieldValidator ID="rfvNombreAlum" runat="server" ControlToValidate="txtnombreAlum" ErrorMessage="Campo obligatorio" ForeColor="Red"></asp:RequiredFieldValidator> 
	<asp:RegularExpressionValidator ID="regexNombreAlum" runat="server" ControlToValidate="txtnombreAlum" ErrorMessage="Solo se permiten letras en el campo Nombre del alumno" ValidationExpression="^[a-zA-Z\s]+$" ForeColor="Red"></asp:RegularExpressionValidator>  
</div>
```

Por favor, ten en cuenta que el ID del `TextBox` debe coincidir con el de `RegularExpressionValidator` y `RequiredFieldValidator`. Esto es necesario para que estos validadores sepan a qué `TextBox` están vinculados.


### 2. Campo que debe ser únicamente un número entero positivo
Para asegurarnos de que el usuario ingrese solamente números enteros positivos en un campo, podemos usar una combinación de `RegularExpressionValidator` y `RequiredFieldValidator` en ASP.NET. Aquí te dejo un ejemplo:

```html
<div class="col-md-6 mb-3">
    <label for="exampleInputContacto">Codigo SACE</label>
    <asp:TextBox ID="txtCodigoSACE" CssClass="form-control" runat="server" autocomplete="off" Text=""></asp:TextBox>
    <asp:RegularExpressionValidator ID="regexCodigoSACE" runat="server" ControlToValidate="txtCodigoSACE"
        ErrorMessage="El campo Codigo SACE debe contener solo números enteros positivos." ValidationExpression="^\d+$"
        ValidationGroup="grupoValidacion" Display="Dynamic"></asp:RegularExpressionValidator>
    <asp:RequiredFieldValidator ID="rfvCodigoSACE" runat="server" ControlToValidate="txtCodigoSACE"
        ErrorMessage="El campo Codigo SACE no puede estar vacío." ValidationGroup="grupoValidacion"
        Display="Dynamic"></asp:RequiredFieldValidator>
    <asp:RequiredFieldValidator ID="rfvPass" runat="server" ControlToValidate="txtCodigoSACE" ErrorMessage="Codigo SACE es obligatorio" ForeColor="Red"></asp:RequiredFieldValidator>
</div>
```
Por favor, ten en cuenta que el ID del `TextBox` debe coincidir con el de `RegularExpressionValidator` y `RequiredFieldValidator`. Esto es necesario para que estos validadores sepan a qué `TextBox` están vinculados. Además, observa que usamos la expresión regular `^\d+$` para validar que la entrada es un número entero positivo.


### 3. Campo de selección obligatoria (dropdown)
En algunos casos, es posible que necesitemos que el usuario seleccione una opción de una lista desplegable. Para asegurarnos de que se ha seleccionado una opción, podemos usar el `RequiredFieldValidator`. Aquí te dejo un ejemplo:

```html
<div class="col-md-6 mb-3">
    <label for="exampleInputOrganizacion">Género</label>
    <asp:DropDownList ID="ddlGenero" CssClass="form-control" runat="server" AppendDataBoundItems="True"
        DataTextField="Text" DataValueField="Value">
        <asp:ListItem Text="Seleccione una opción" Value=""></asp:ListItem>
        <asp:ListItem Value="Hombre">Hombre</asp:ListItem>
        <asp:ListItem Value="Mujer">Mujer</asp:ListItem>
        <asp:ListItem Value="Prefiero no decirlo">Prefiero no decirlo</asp:ListItem>
        <asp:ListItem Value="Gay">Gay</asp:ListItem>
        <asp:ListItem Value="Lesbiana">Lesbiana</asp:ListItem>
    </asp:DropDownList>
    <asp:RequiredFieldValidator ID="rfvGenero" runat="server" ControlToValidate="ddlGenero"
        ErrorMessage="Debe seleccionar una opción en el campo Género" ForeColor="Red"></asp:RequiredFieldValidator>
</div>
```
Por favor, ten en cuenta que el ID del `DropDownList` debe coincidir con el de `RequiredFieldValidator`. Esto es necesario para que el validador sepa a qué `DropDownList` está vinculado.
