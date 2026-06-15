## Task 1

Command: grep -Ec '^[^#]' firewall.log

Result: 100000

Explanation: ^ ancla al inicio de línea. [^#] es una clase negada que coincide con cualquier carácter que NO sea #, por lo que las 4 líneas de encabezado son ignoradas y solo se cuentan los 100000 eventos reales.

## Task 2

Command: grep -Ec '^[^ ]+ [^ ]+ (DROP|REJECT) ' firewall.log

Result: 60156

Explanation: ^[^ ]+ [^ ]+ consume los campos date y time. Luego (DROP|REJECT) usa alternación dentro de un grupo para coincidir con una de las dos acciones. El espacio al final asegura que se ancle al campo action completo y no a texto parcial.

