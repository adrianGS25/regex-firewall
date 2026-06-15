## Task 1

Command: grep -Ec '^[^#]' firewall.log

Result: 100000

Explanation: ^ ancla al inicio de línea. [^#] es una clase negada que coincide con cualquier carácter que NO sea #, por lo que las 4 líneas de encabezado son ignoradas y solo se cuentan los 100000 eventos reales.

