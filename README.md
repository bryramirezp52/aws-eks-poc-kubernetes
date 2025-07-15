# 🏗️ Arquitectura de Contenedores en AWS con Kubernetes - Prueba Parcial 3

Este repositorio documenta el diseño, despliegue y validación de una arquitectura distribuida y resiliente para una aplicación crítica del Banco Etheria. Se propone una solución basada en Amazon EKS, AWS Fargate, Amazon SQS y ElastiCache, y se ejecuta una Prueba de Concepto (POC) para validar su viabilidad.

> 🔍 **Estado actual**: Se logró desplegar una aplicación básica en EKS. Sin embargo, el balanceador de carga (ELB) y el escalado automático (HPA) fallaron durante las pruebas. Este informe refleja tanto los aciertos como los límites de la implementación práctica.

---

## 📐 Arquitectura Propuesta

- **Orquestación**: Amazon EKS sobre Fargate.
- **Desacoplamiento de transacciones**: Amazon SQS.
- **Cache distribuido para lecturas**: Amazon ElastiCache (Redis).
- **Base de datos**: Amazon RDS con Multi-AZ y Read Replicas.
- **Seguridad**: Zero Trust con Network Policies, IRSA e IAM.
- **Observabilidad**: CloudWatch Logs, Container Insights y AWS X-Ray.

📊 [Ver Diagrama en Lucidchart](https://lucid.app/lucidchart/f6a0ad49-0090-4797-a24d-cdb98cf6f4c9/view)

---

## 🚀 Prueba de Concepto (POC)

Se desplegó una aplicación 2048 con dos réplicas en un clúster EKS y se intentó exponerla vía ELB usando un `Service` tipo LoadBalancer. Ante fallos en la provisión del ELB, se utilizó `ngrok` como solución alternativa.

Además, se intentó activar un **Horizontal Pod Autoscaler (HPA)** para escalar los pods en función del uso de CPU, pero el mecanismo no se activó durante pruebas de carga.

---

## 🧪 Resultados y Pruebas Realizadas

- ✅ Despliegue exitoso del clúster y aplicación base.
- ❌ Fallo en la creación automática del ELB.
- ❌ El HPA no reaccionó ante el estrés simulado.
- ✅ Validación de auto-reparación de pods eliminados manualmente.

---

## 📚 Lecciones Aprendidas

1. **Validación incremental es clave**: primero asegurar ELB y HPA antes de integrar todo.
2. **Networking y permisos en AWS son críticos**: errores en etiquetado de subredes e IAM causaron fallos.
3. **La teoría no siempre traduce en éxito inmediato**: pero cada error fue una oportunidad de aprendizaje técnico real.

---

## ✅ Recomendaciones Futuras

- Corregir la configuración de red y permisos para ELB.
- Ejecutar pruebas controladas de escalabilidad (HPA).
- Integrar gradualmente SQS y ElastiCache tras validar la base.

---

## 👨‍💻 Autor

**Bryan Ramírez Palacios**  
Estudiante de Ingeniería en Infraestructura y Plataformas Tecnológicas  
Sección: DIY7121_003V  
Fecha: Junio 2025
