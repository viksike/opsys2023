3.
echo "Sisesta nimi: "
read nimi
echo "Sisesta eriala: "
read eriala
echo "Sisesta matriklinumber: "
read number
echo "Sisestati: $nimi, $eriala, $number"

![Screenshot 2023-11-27 at 10 43 01](https://github.com/viksike/opsys2023/assets/144438506/30eb6470-846a-4361-b447-ea2100659d3b)

4.
#!/bin/sh -x või #!/bin/sh
a=$1
b=$2
for i in *.$a; do
  if [ "${i##*.}" = "$a" ]; then
    uusnimi="${i%.*}.$b"
    mv "$i" "$uusnimi"
  fi
done
![Screenshot 2023-11-27 at 11 11 55](https://github.com/viksike/opsys2023/assets/144438506/30672d86-91d0-4da9-a3c8-18937028961b)

5.
#!/bin/bash

# Kontrollime, kas on antud argument
if [ -z "$1" ]; then
    echo "Viga: puudub argument"
    exit 1
fi

# Leiame protsessi
ps -A | while read line; do
    # Eemaldame korduvad tühikud
    line=$(echo "$line" | tr -s ' ')

    # Kontrollime, kas rida algab protsessi nimega
    if [[ "$line" =~ ^"$1" ]]; then
        # Leiame protsessi PID
        pid=$(echo "$line" | cut -d ' ' -f2)

        # Väljastame tulemuse
        echo "PID: $pid, nimi: $line"
    fi
done

![Screenshot 2023-12-04 at 10 21 07](https://github.com/viksike/opsys2023/assets/144438506/5745ab91-e00d-475a-9a7c-7753015eb768)

6.
