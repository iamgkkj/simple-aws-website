# Simple AWS Website

A simple, responsive website demonstrating AWS EC2 deployment with Apache middleware. This project serves as a learning resource for AWS cloud deployment and web hosting basics.

## Features

- 🎨 Clean, modern design with dark/light mode toggle
- 📱 Responsive layout that works on all devices
- 🌙 Theme persistence using localStorage
- 📖 Comprehensive AWS EC2 and Apache deployment guide
- 🔗 Social links in footer (GitHub & LinkedIn)
- 🚀 Ready for cloud deployment

## Local Development

### Prerequisites

- A web browser (Chrome, Firefox, Safari, etc.)
- Text editor (VS Code, Sublime Text, etc.)
- (Optional) Python 3 for local server

### Running Locally

1. Clone or download the project files
2. Open `index.html` directly in your browser, or
3. Start a local server:

   ```bash
   # Using Python (built-in)
   python3 -m http.server 8000

   # Or using Node.js (if available)
   npx http-server -p 8000
   ```

4. Open http://localhost:8000 in your browser

## AWS EC2 Deployment

### Prerequisites

- AWS Account with appropriate permissions
- SSH client (built-in on Linux/Mac, PuTTY on Windows)
- Key pair for EC2 instance access

### Step-by-Step Deployment

#### 1. Launch EC2 Instance

1. Sign in to the [AWS Management Console](https://console.aws.amazon.com/)
2. Navigate to EC2 Dashboard
3. Click "Launch Instance"
4. Choose AMI:
   - **Amazon Linux 2** (recommended) or **Ubuntu Server**
5. Select instance type: `t2.micro` (free tier eligible)
6. Configure security groups:
   - **HTTP**: Port 80, Source: 0.0.0.0/0
   - **SSH**: Port 22, Source: Your IP or 0.0.0.0/0
7. Launch instance and download key pair (.pem file)

#### 2. Connect to Instance

```bash
# Set correct permissions on key
chmod 400 your-key-pair.pem

# Connect via SSH
ssh -i your-key-pair.pem ec2-user@your-instance-public-ip
```

#### 3. Install Apache

**For Amazon Linux 2:**
```bash
sudo yum update -y
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
```

**For Ubuntu:**
```bash
sudo apt update
sudo apt upgrade -y
sudo apt install apache2 -y
sudo systemctl start apache2
sudo systemctl enable apache2
```

#### 4. Deploy Website

```bash
# Upload files to web server directory
# Option 1: Using SCP
scp -i your-key-pair.pem -r . ec2-user@your-instance-public-ip:/tmp/website

# Option 2: Using rsync (if available)
rsync -avz -e "ssh -i your-key-pair.pem" . ec2-user@your-instance-public-ip:/tmp/website

# On the EC2 instance:
sudo cp -r /tmp/website/* /var/www/html/
sudo chown -R apache:apache /var/www/html/  # Amazon Linux
# OR
sudo chown -R www-data:www-data /var/www/html/  # Ubuntu
```

#### 5. Access Your Website

Open your browser and navigate to:
```
http://your-instance-public-ip
```

### Security Best Practices

- **Security Groups**: Only open necessary ports (80 for HTTP, 22 for SSH)
- **SSH Access**: Use key pairs instead of passwords
- **Instance Management**: Stop instances when not in use to avoid charges
- **Updates**: Keep your system updated regularly

### Cost Optimization

- Use **t2.micro** instances (free tier eligible)
- Stop instances when not actively using them
- Monitor usage in AWS Cost Explorer
- Set up billing alerts

## Project Structure

```
simple-aws-website/
├── index.html          # Main website file
├── README.md           # This file
└── .git/              # Git repository (if applicable)
```

## Technologies Used

- **HTML5**: Semantic markup and structure
- **CSS3**: Styling with responsive design and themes
- **JavaScript**: Theme toggle functionality
- **Font Awesome**: Icons for theme toggle and social links

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test locally
5. Submit a pull request

## License

This project is open source and available under the [MIT License](LICENSE).

## Support

For questions or issues:
- 📧 Create an issue on GitHub
- 🔗 Connect on [LinkedIn](https://www.linkedin.com/in/gopal-krishn-khoth-cse712003)
- 📚 Check AWS documentation

---

**Created by Gopal** | [GitHub](https://github.com/iamgkkj) | [LinkedIn](https://www.linkedin.com/in/gopal-krishn-khoth-cse712003)
