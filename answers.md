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

## Task 4

Command: grep -Ec ' [0-9]{7}$' firewall.log

Result: 2343

Explanation: [0-9]{7} usa el cuantificador {n} para exigir exactamente 7 dígitos consecutivos. El ancla $ al final de línea garantiza que el campo size termine justo ahí sin dígitos adicionales, por lo que solo coinciden valores >= 1,000,000.

## Task 5

Command: grep -E '^[^#]' firewall.log | sed -E 's/^([0-9-]+) [^ ]+ ([^ ]+) ([^ ]+) .*/\1 \2 \3/' | head -5

Result:
2018-05-25 FORWARD TCP
2018-02-22 FORWARD UDP
2018-03-20 REJECT UDP
2018-11-08 REJECT TCP
2018-07-24 REJECT TCP

Explanation: Three capture groups () capture: \1 = date ([0-9-]+), \2 = action ([^ ]+) skipping the time field, and \3 = protocol ([^ ]+). The substitution s/pattern/\1 \2 \3/ rebuilds the line using only those three fields.

## Task 6

Command: grep -Ec ' ACCEPT TCP .* 80 [0-9]+$' firewall.log

Result: 93

Explanation: ACCEPT TCP matches the action and protocol fields literally. .* consumes all intermediate fields (IPs and source port). 80 followed by a space and [0-9]+$ anchors the value 80 to the dst-port field, which is the second-to-last field just before the size at the end of the line.