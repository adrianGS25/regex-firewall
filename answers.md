## Task 1

Command: grep -Ec '^[^#]' firewall.log

Result: 100000

Explanation: ^ ancla al inicio de línea. [^#] es una clase negada que coincide con cualquier carácter que NO sea #, por lo que las 4 líneas de encabezado son ignoradas y solo se cuentan los 100000 eventos reales.

## Task 2

Command: grep -Ec '^[^ ]+ [^ ]+ (DROP|REJECT) ' firewall.log

Result: 60156

Explanation: ^[^ ]+ [^ ]+ consume los campos date y time. Luego (DROP|REJECT) usa alternación dentro de un grupo para coincidir con una de las dos acciones. El espacio al final asegura que se ancle al campo action completo y no a texto parcial.

## Task 3

Command: grep -Ec ' 11\.' firewall.log

Result: 33217

Explanation: El espacio antes de 11 asegura que estamos al inicio del campo src-ip. \. escapa el punto para que sea tratado literalmente como un punto real que separa octetos, y no como metacarácter que coincide con cualquier carácter.