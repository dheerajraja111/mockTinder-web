# MockTinder

# Deployment

    - Signup on AWS
    - Launch an instance
    - Go to SSH Client
    - chmod 400 "mockTinder-secret.pem"
    - ssh -i "mockTinder-secret.pem" ubuntu@ec2-51-20-132-133.eu-north-1.compute.amazonaws.com
    - Install Node version
    - Git clone
    - Frontend
        - npm install
        - npm build
        - sudo apt update
        - sudo apt install nginx
        - sudo systemctl start nginx
        - sudo systemctl enable nginx
        - Copy code from dist to /var/www/html
        - sudo scp -r dist/* /var/www/html/
        - Enable port :80 of instance
    - Backend
        - Add ec2 instance public ip on mongodb server
        - npm install pm2 -g
        - pm2 start npm --name "mocktinder-backend" -- start
        - Check logs using pm2 logs
        - pm2 list, pm2 stop <name>, pm2 delete <name>
        - config nginx -/etc/nginx/sites-available/default
        - Restart nginx - sudo systemctl restart nginx
        -
    - App running on
        - Frontend: http://13.61.182.43/ => http://mocktinder.com
        - Backend: http://13.61.182.43:7777 => http://mocktinder.com/api

    - nginx config
        - server_name 13.61.182.43

            location /api/ {
                proxy_pass http://localhost:7777/;
                proxy_http_version 1.1;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection 'upgrade';
                proxy_set_header Host $host;
                proxy_cache_bypass $http_upgrade;
            }

# Adding a custom domain name

    - purchased domain name (ex: godaddy)
    - signup on cloudfare and add a new domain name
    - change the nameservers on godaddy and point it to cloudfare
    - wait for some time till nameservers are updated
    - DNS record: A mocktinder.in <ip:address>

# RazorPay Integration

    - RazorPay signup and complete KYC
    - Created UI for premium
    - Create API for create order in backend
    - Added key and secret in env file
    - Initialized Razor pay in utils
    - Creating order on razor pay
    - create schema and model
    - saved the order in payment collection
    - Setup razorpay webhook
    - Ref: https://github.com/razorpay/razorpay-node/tree/master/documents
    - Ref: https://razorpay.com/docs/payments/server-integration/nodejs/integration-steps/integrate-with-razorpay-payment-gateway
    - Ref: https://razorpay.com/docs/webhooks/validate-test/
    - Ref: https://razorpay.com/docs/webhooks/payloads/payments/

# Real time chat using web socket (socket.io)

    - Setup socket.io in backend
    - npm i socket.io
    - Setup socket in frontend
    - npm i socket.io-client
    - Initialize the chat
    - createSocketConnection
    - Listen to events
