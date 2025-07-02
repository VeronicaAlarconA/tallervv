name: Deploy Monitoring Stack

on:
  push:
    paths:
      - 'monitoring/**'
      - 'docker-compose.yml'

jobs:
  deploy-monitoring:
    name: Deploy Prometheus and Grafana to EC2
    runs-on: ubuntu-latest

    steps:
    - name: Deploy to EC2
      uses: appleboy/ssh-action@v1.0.0
      with:
        host: ${{ secrets.EC2_HOST }}
        username: ${{ secrets.EC2_USER }}
        key: ${{ secrets.EC2_SSH_KEY }}
        script: |
          # Si el directorio no existe, clonamos el repositorio
          if [ ! -d ~/tallervv ]; then
            git clone https://github.com/veronicaalarcona/tallervv.git ~/tallervv
          fi
          
          cd ~/tallervv
          git pull origin main
          
          # Si el archivo prometheus.yml no existe, crearlo
          if [ ! -f ./monitoring/prometheus/prometheus.yml ]; then
            echo "Creando prometheus.yml..."
            cat <<EOF > ./monitoring/prometheus/prometheus.yml
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'prometheus'
    static_configs:
      - targets: ['localhost:9090']
EOF
          fi
          
          # Levantar Prometheus y Grafana
          docker-compose down -v
          docker-compose up -d prometheus grafana
