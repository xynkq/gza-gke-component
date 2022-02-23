gcloud iam service-accounts create erica-gke-workloadidentity

kubectl create serviceaccount --namespace default erica-gke-workloadidentity

gcloud iam service-accounts add-iam-policy-binding --role roles/iam.workloadIdentityUser --member "serviceAccount:swit-cloud-erica.svc.id.goog[default/erica-gke-workloadidentity]" erica-gke-workloadidentity@swit-cloud-erica.iam.gserviceaccount.com

k annotate serviceaccount --namespace default erica-gke-workloadidentity iam.gke.io/gcp-service-account=erica-gke-workloadidentity@swit-cloud-erica.iam.gserviceaccount.com

# role 최초 부여

gcloud projects add-iam-policy-binding swit-cloud-erica --member serviceAccount:erica-gke-workloadidentity@swit-cloud-erica.iam.gserviceaccount.com --role roles/container.admin

# 추가 role 의 경우 GCP 웹 콘솔에서 가능