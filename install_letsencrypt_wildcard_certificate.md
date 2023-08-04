`sudo certbot certonly --manual --preferred-challenges dns` (use --test-cert for testing the certbot first)

when asked for domain name:
domain.tld *.domain.tld

create required dns txt record (_acme-challenge.domain.tld) with provided value

to check dns record:
`dig -t txt +short _acme-challenge.domain.tld` (or with mxtoolbox or whatever)

when successful continue (usually takes no more then 5 minutes)
copy provided certificate file addresses to somewhere, they will be needed

to check certificate file:
`sudo openssl x509 -in /address/for/certificate/file/fullchain.pem -text -noout`

on nginx config add:

    ssl_certificate /address/for/certificate/file/fullchain.pem;
    ssl_certificate_key /address/for/certificate/file/privkey.pem;
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    ssl_ciphers HIGH:!aNULL:!MD5;

to test nginx configuration:
`sudo nginx -t`

if successful:
`sudo service nginx reload`

you may want to:

    if ($host = whatever.domain.tld) { #only this domain redirects to https
        return 307 https://$host$request_uri;
    }

or

`return 307 https://$host$request_uri; #everything redirects to https`

**307 is used instead of 301 because 301 - 302 redirects convert post requests into get...**

