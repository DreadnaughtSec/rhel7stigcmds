# rhel7stigcmds
Better commands for checking RHEL 7 STIGs

## v-71849 (produces copy/paste commands to run)
`files=($(for i in `rpm -Va | grep '^.M' | cut -d " " -f4,5`;do for j in `rpm -qf $i`;do rpm -ql $j --dump | cut -d " " -f1,5,6,7 | grep $i | awk '{print $1}';done;done)); packages=($(for i in "${files[@]}"; do rpm -qf "$i";done;));output="";for j in "${packages[@]}"; do output+="rpm -setperms $j;";output+=$'\n';output+="rpm --setugids $j;";output+=$'\n';done;echo "$output" | sort -d | uniq;
`

## v-72017
`folders=($(ls -ld $(egrep ':[0-9]{4}' /etc/passwd | cut -d: -f6)|awk '{print $9}'));for i in "${folders[@]}"; do chmod 0750 "$i"; done;`

## v-72033
`files=($(ls -al /home/*/.* | grep "./" | grep -v "/.:\|/..:\|mozilla"| awk '{print $9}'));for i in "${files[@]}"; do chmod 0740 "$i";done;`

## v-72069/72071/72073 (all at once)
`file=$(find / -name aide.conf 2>/dev/null);cat $file | grep "acl\|xattrs\|sha512";`

## v-72075
`file=$(find / -name grub.cfg 2>/dev/null);grep -c menuentry $file;grep "set root" $file;`

## v-72089
`grep -iw log_file /etc/audit/auditd.conf;partsize=$(df -h /var/log/audit | awk '{print $2}');echo "$partsize";grep -iw "space_left" /etc/audit/auditd.conf;`

## v-72211
`grep "imtcp\|imudp\|imrelp" /etc/rsyslog.conf`

## v-72417
`rpm -qa | grep "esc-\|authconfig\|pam_pkcs11"`
