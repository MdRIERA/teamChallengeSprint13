# teamChallengeSprint13

## 1️⃣ Obtener el informe del crimen
Se busca el informe del asesinato ocurrido el 15 de enero de 2018 en SQL City.

SELECT *
FROM crime_scene_report
WHERE date = 20180115
  AND type = 'murder'
  AND city = 'SQL City';

<img width="852" height="142" alt="image" src="https://github.com/user-attachments/assets/458ae38f-5050-458c-9e00-2cc7966d1bef" />

---

## 2️⃣ Identificar al primer testigo
Se obtiene a la persona que vive en la última casa de Northwestern Dr.

SELECT *
FROM person
WHERE address_street_name = 'Northwestern Dr'
ORDER BY address_number DESC
LIMIT 1;

<img width="716" height="101" alt="image" src="https://github.com/user-attachments/assets/c5f02978-429d-488b-bfc7-2a1eba60b1a2" />

---

## 3️⃣ Identificar a la segunda testigo
Se localiza a Annabel, que vive en Franklin Ave.

SELECT *
FROM person
WHERE name LIKE 'Annabel%'
  AND address_street_name = 'Franklin Ave';

<img width="690" height="95" alt="image" src="https://github.com/user-attachments/assets/a6beabed-9d54-4a45-806d-d39a24f541ed" />

---

## 4️⃣ Consultar las entrevistas de los testigos
Se revisan las declaraciones para obtener pistas del asesino.

SELECT person_id, transcript
FROM interview
WHERE person_id IN (14887, 16371);

<img width="865" height="200" alt="image" src="https://github.com/user-attachments/assets/eb544744-257d-4eea-a2ec-32eac2ae87b2" />

---

## 5️⃣ Buscar socios del gimnasio sospechosos
Se filtran socios GOLD del gimnasio cuyo número de membresía empieza por "48Z".

SELECT *
FROM get_fit_now_member
WHERE membership_status = 'gold'
  AND id LIKE '48Z%';

<img width="687" height="176" alt="image" src="https://github.com/user-attachments/assets/cec7e243-bdc7-4a77-8522-a3294a164109" />

---

## 6️⃣ Ver quién estuvo en el gimnasio el día clave
Se comprueba qué sospechosos estuvieron en el gimnasio el 9 de enero de 2018.

SELECT *
FROM get_fit_now_check_in
WHERE check_in_date = 20180109
  AND membership_id IN ('48Z7A', '48Z55');

<img width="496" height="151" alt="image" src="https://github.com/user-attachments/assets/ec977b44-9885-4adf-b984-2e0c671deee6" />

---

## 7️⃣ Filtrar matrículas relacionadas con el crimen
Se buscan carnés de conducir con matrículas que contengan "H42W".

SELECT *
FROM drivers_license
WHERE plate_number LIKE '%H42W%';

<img width="724" height="205" alt="image" src="https://github.com/user-attachments/assets/8e2eecb8-9834-4e47-88b3-659cebf2009d" />

---

## 8️⃣ Identificar al asesino
Se cruzan personas sospechosas con su matrícula para identificar al culpable.

SELECT p.name, d.plate_number
FROM person p
JOIN drivers_license d ON p.license_id = d.id
WHERE p.id IN (28819, 67318)
  AND d.plate_number LIKE '%H42W%';

<img width="248" height="104" alt="image" src="https://github.com/user-attachments/assets/bd2fb7bf-5677-413b-ae84-743f0967b61d" />

---

## 9️⃣ Registrar la solución
Se inserta el nombre del asesino y se valida la solución.

INSERT INTO solution VALUES (1, 'Jeremy Bowers');
SELECT value FROM solution;

<img width="841" height="126" alt="image" src="https://github.com/user-attachments/assets/e123061f-3ae1-41f8-b206-2a2d2094a3b7" />
