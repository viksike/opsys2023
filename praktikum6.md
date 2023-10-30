# Praktikum 6 aruanne

Kuuendas praktikumis lahendasime protsesside ja signaalide praktikumi. Selleks kulus päris palju aega, sest minu jaoks oli see vägagi arusaamatu teema. Üritasin nii palu aru saada kui võimalik ja küsisin abi nii juhendajalt, kursakaaslastelt kui ka ChatGPT'lt. Järgnev on mu lahendus.

1. 
![Screenshot 2023-10-16 at 11 14 43](https://github.com/viksike/opsys2023/assets/144438506/2ceffd50-841d-4382-9867-86cb321c4cf9)

2.
![Screenshot 2023-10-16 at 11 31 04](https://github.com/viksike/opsys2023/assets/144438506/70cb33b4-51d1-427b-bec2-887fb905aec9)

3. ps -axu | grep daemon | awk '{for(i=11;i<=NF;++i)print $i}' | tr -s ' ' '\n' | grep "daemon"
![Screenshot 2023-10-30 at 10 37 10](https://github.com/viksike/opsys2023/assets/144438506/bb8f3032-3627-4851-89f4-99ef7ad5b8ab)

4. ip a | grep 'inet ' | grep -v '127.0.0.1' | awk '{print $2}' | cut -d'/' -f1 > ipaddress.txt
![Screenshot 2023-10-30 at 10 37 10](https://github.com/viksike/opsys2023/assets/144438506/5ab07f9e-df0a-4c32-963c-264563ab0ee0)
