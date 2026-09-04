# Client Recommendations

## Client A — Startup Company

**Scenario:** A startup company wants to launch a new mobile application. Their budget is limited, but they expect rapid growth within the next few years.

**Recommended Platform:**

AWS

**Explanation:**

Para sa isang startup na limited yung budget pero gusto ring mag-grow nang mabilis, si AWS yung pinaka-fit dahil sa pay-as-you-go pricing niya. Ibig sabihin, babayaran mo lang yung actual na nagamit mo, kaya hindi mo kailangan maglabas agad ng malaking amount sa simula. Bukod dun, dahil sobrang daming services ng AWS, madali rin siyang i-scale habang lumalaki yung business, from a simple application hanggang sa mas complex na system. Marami rin siyang documentation and community support, kaya mas easy para sa small team na matuto at mag-troubleshoot on their own.
  
**Services to use:**

- Amazon EC2 – para sa pag-host ng mobile app backend, so dito tatakbo yung main backend ng app.
- Amazon S3 – para sa pag-store ng data, images, videos, at iba pang media files.
- AWS Lambda – para sa serverless functions, kaya makakatipid sa cost lalo na habang maliit pa yung traffic ng app.

## Client B — University

**Scenario:** A university already uses Windows Server, Microsoft 365, and Active Directory. The university wants to migrate some services to the cloud.

**Recommended Platform:**

Microsoft Azure

**Explanation:**

Dahil gumagamit na yung university ng Windows Server, Microsoft 365, at Active Directory, si Microsoft Azure yung pinaka-fit na cloud platform para sa kanila. Directly integrated kasi yung Azure sa mga Microsoft products na gamit na nila, kaya mas easy yung pag-move to the cloud without changing yung buong existing system ng university. Plus, dahil compatible siya sa Active Directory through Microsoft Entra ID, mas simple rin yung pag-manage ng user accounts and permissions ng students at faculty.

**Services to use:**

- Azure Virtual Machines – para sa pag-host ng mga school applications or systems na gustong ilipat sa cloud.
- Microsoft Entra ID – para sa pag-manage ng user accounts and access, since connected siya sa existing Active Directory ng university.
- Azure Blob Storage – para sa pag-store ng files, records, at iba pang university data.

## Client C — AI Research Company

**Scenario:** A research company develops Artificial Intelligence and Machine Learning applications that require high-performance computing.

**Recommended Platform:**

Google Cloud Platform (GCP)

**Explanation:**

Para sa isang company na nagde-develop ng AI at Machine Learning applications, si Google Cloud Platform yung pinaka-fit dahil known talaga siya sa data analytics at artificial intelligence. Halos 90% ng generative AI startups around the world ay gumagamit ng GCP, kaya makikita na trusted din siya ng AI industry. Meron din itong specialized tools like BigQuery at Vertex AI na useful for analyzing large datasets at pag-develop ng machine learning models. Dahil dito, mas mabilis and efficient yung workflow ng research team.

**Services to use:**

- Vertex AI – para sa pag-build, pag-train, at pag-deploy ng machine learning models.
- BigQuery – para sa mabilis na pag-analyze ng malaking volume ng research data.
- Compute Engine – para sa high-performance computing na kailangan kapag nagta-train ng AI models.

## Client D — Global E-Commerce Company

**Scenario:** A multinational online shopping company serves customers around the world and requires highly available infrastructure with automatic scaling.

**Recommended Platform:**

AWS

**Explanation:**

Para sa isang global e-commerce company na may customers from different parts of the world, si AWS yung pinaka-fit dahil sa malaking global infrastructure niya na may 39 regions at 124+ availability zones. Dahil dito, mas mabilis and reliable yung access ng customers kahit nasa ibang bansa sila. Kapag nagkaroon naman ng problem sa isang zone, hindi agad maaapektuhan yung buong system dahil may ibang zones na pwedeng mag-handle. May mga services din ang AWS na built for scalability, kaya kaya niyang mag-handle ng sudden increase sa traffic, especially kapag may big sales or promo events.

**Services to use:**

- Amazon EC2 with Auto Scaling – para automatic na madagdagan or mabawasan yung compute resources depende sa traffic ng website.
- Amazon CloudFront – para mas mabilis ma-deliver yung website content sa customers kahit nasa iba’t ibang parts ng world.
- Amazon RDS – para sa reliable and scalable database na mag-store ng transactions at customer data.
