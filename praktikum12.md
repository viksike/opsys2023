# Praktikum 12 aruanne
12 praktikum oli loogiline ja huvitav. AI abi oli ka hea kasutada, kui endal mõte kokku jooksis. Aega kulus kokku umbes tund.


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
#!/bin/sh -x
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
if [ -z "$1" ]; then
    echo "Viga: puudub argument"
    exit 1
fi

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
#!/bin/bash

power() {
    local base=$1
    local exponent=$2
    if [ $exponent -eq 0 ]; then
        echo 1
    else
        echo $((base * $(power $base $((exponent - 1)))))
    fi
}
result=$(power $1 $2)
echo "$result"
![Screenshot 2023-12-04 at 10 29 25](https://github.com/viksike/opsys2023/assets/144438506/8d3e6e20-3d0f-4f47-a856-adcf4a9819ad)
7.
![Screenshot 2023-12-04 at 10 33 40](https://github.com/viksike/opsys2023/assets/144438506/8b0eae2b-a690-47af-ad70-44f959a0f4df)

