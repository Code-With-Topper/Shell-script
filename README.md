# 🐚 Shell Practicals — Complete Collection (Online Bash Compiler Ready)

This document includes all Shell Practicals (1 – 9) rewritten to work directly on **online Bash compilers**.  
✅ Just copy each script block and paste into a compiler like [OnlineGDB – Bash](https://www.onlinegdb.com/online_bash_shell).  
✅ No need for `chmod` or separate files.

---

## 🧭 Practical 1 — General Purpose & File System Commands
(Use these directly in terminal)
```
cal
date
echo "Hello World"
banner "WELCOME"
bc
script
passwd
who
uname
tty
stty
clear
exit
pwd
cd
mkdir testdir
rmdir testdir
ls -l
```

---

## 📂 Practical 2 — Handling Files and Processes
```
cat file.txt
cp file1 file2
rm file.txt
mv old new
more file.txt
lp file.txt
file file.txt
wc file.txt
od -c file.txt
cmp file1 file2
comm file1 file2
diff file1 file2
ps
kill <pid>
at now + 1 minute
batch
time ls
```

---

## 🧾 Practical 3 — Simple Filters
```
pr file.txt
head -n 5 file.txt
tail -n 5 file.txt
cut -d" " -f1 file.txt
paste file1 file2
sort file.txt
uniq file.txt
tr a-z A-Z
```

---

## ⚙️ Practical 4 — File Attributes & Filters (grep/sed)
```
grep "text" file.txt
egrep "pattern" file.txt
fgrep "fixedstring" file.txt
sed 's/old/new/g' file.txt

chmod 755 script.sh
chown user file
chgrp group file
```

---

## 🔢 Practical 5 — Basic Programming Using Shell Script
```bash
# 1) Sum, Product, Average
read -r a b c d
sum=$((a+b+c+d))
product=$((a*b*c*d))
avg=$(echo "scale=3; $sum/4" | bc -l)
echo "Sum=$sum  Product=$product  Average=$avg"
```

```bash
# 2) Simple Calculator
while true; do
echo "1.Add 2.Sub 3.Mul 4.Div 5.Exit"
read -r ch
case $ch in
1) read -r x y; echo "Result=$(echo "$x+$y"|bc -l)";;
2) read -r x y; echo "Result=$(echo "$x-$y"|bc -l)";;
3) read -r x y; echo "Result=$(echo "$x*$y"|bc -l)";;
4) read -r x y; [ "$y" = 0 ] && echo "Div by 0!" || echo "Result=$(echo "scale=3;$x/$y"|bc -l)";;
5) break;;
*) echo "Invalid";;
esac
done
```

```bash
# 3) Gross Salary
read -r basic
da=$(echo "$basic*0.10"|bc)
hra=$(echo "$basic*0.20"|bc)
gross=$(echo "$basic+$da+$hra"|bc)
echo "Gross Salary=$gross"
```

```bash
# 4) Factorial
read -r n; f=1
for ((i=2;i<=n;i++)); do f=$((f*i)); done
echo "Factorial=$f"
```

```bash
# 5) Max & Min from command-line args
max=$1; min=$1
for v in "$@"; do
((v>max))&&max=$v
((v<min))&&min=$v
done
echo "Max=$max Min=$min"
```

---

## 🔁 Practical 6 — Loops
```bash
# 1) Series 1+x+x²+x³+x⁴
read -r x; s=0
for i in {0..4}; do s=$(echo "$s+($x^$i)"|bc -l); done
echo "Sum=$s"
```

```bash
# 2) Sum of arguments
sum=0; for n in "$@"; do sum=$((sum+n)); done
echo "Sum=$sum"
```

```bash
# 3) Reverse String
read -r s; echo "$s" | rev
```

```bash
# 4) Sum of digits
read -r n; s=0
while [ "$n" -gt 0 ]; do d=$((n%10)); s=$((s+d)); n=$((n/10)); done
echo "Sum of digits=$s"
```

```bash
# 5) String Operations
read -r s
read -r start
read -r len
read -r ch
echo "Length=${#s}"
echo "Substring=${s:$start:$len}"
pos=$(expr index "$s" "$ch")
echo "Position=$pos"
```

---

## ⚖️ Practical 7 — Control Structures
```bash
# 1) Palindrome
read -r s
[ "$s" = "$(echo "$s"|rev)" ] && echo "Palindrome" || echo "Not palindrome"
```

```bash
# 2) Prime Check
read -r n
p=1; for ((i=2;i*i<=n;i++)); do ((n%i==0))&&p=0&&break; done
((p&&n>1))&&echo "Prime"||echo "Not prime"
```

```bash
# 3) Character Type
read -r c
case $c in
[0-9]) echo "Digit";;
[a-z]) echo "Lowercase";;
[A-Z]) echo "Uppercase";;
*) echo "Other";;
esac
```

```bash
# 4) Sort Numbers
read -ra arr
printf "%s\n" "${arr[@]}" | sort -n
```

```bash
# 5) Check File Type
read -r f
[ -f "$f" ] && echo "Ordinary file" || echo "Not ordinary"
```

---

## 🧮 Practical 8 — Judge Database Manager
```bash
DB="judge.txt"; [ -f "$DB" ]||echo "Judge|Court|City|Cases|Total" >"$DB"

add(){ read -r j c city cj tc; echo "$j|$c|$city|$cj|$tc" >>"$DB"; }
view(){ column -t -s"|" "$DB"; }
count(){ echo "Records: $(($(wc -l<$DB)-1))"; }
highest(){ awk -F'|' 'NR>1{if($4>m){m=$4; n=$1}}END{print n" ("m")"}' "$DB"; }
totalahm(){ awk -F'|' 'NR>1&&tolower($3)=="ahmedabad"{s+=$5}END{print s}' "$DB"; }

while true; do
echo "1.Add 2.View 3.Count 4.Highest 5.Ahmedabad Total 6.Exit"
read -r ch
case $ch in
1)add;;
2)view;;
3)count;;
4)highest;;
5)totalahm;;
6)exit;;
*)echo "Invalid";;
esac
done
```

---

## 📚 Practical 9 — Library Management System
```bash
DB="library.txt"; [ -f "$DB" ]||echo "AccNo|Title|Author|Edition|Publisher" >"$DB"

add(){ read -r a t au e p; echo "$a|$t|$au|$e|$p" >>"$DB"; }
view(){ column -t -s"|" "$DB"; }
search(){ read -r q; grep -i "$q" "$DB" || echo "Not found"; }
delete(){ read -r a; grep -v "^$a|" "$DB" >tmp && mv tmp "$DB"; }
count(){ echo "Records: $(($(wc -l<$DB)-1))"; }

while true; do
echo "1.Add 2.View 3.Search 4.Delete 5.Count 6.Exit"
read -r ch
case $ch in
1)add;;
2)view;;
3)search;;
4)delete;;
5)count;;
6)exit;;
*)echo "Invalid";;
esac
done
```

---

## ✅ How to Use
1. Go to **OnlineGDB → Bash Shell**
2. Paste the desired block
3. Click ▶️ **Run**
4. For menu-based scripts, use the interactive terminal
