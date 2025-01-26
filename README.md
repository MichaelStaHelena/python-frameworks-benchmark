# Rinha de Python Frameworks  
## A project to compare and benchmark Python web frameworks.  
### Inspired by [rinha-de-backend](https://github.com/zanfranceschi/rinha-de-backend-2023-q3)  

---

## **Frameworks**  
- [Bottle](bottle/)  
- [FastAPI](fastapi/)  
- [Flask](flask/)  
- [Pyramid](pyramid/)  
- [Quart](quart/)  
- [Sanic](sanic/)  

---

## **Setup**  
1. Clone the repository:  
   ```bash
   git clone https://github.com/MichaelStaHelena/rinha-de-python-frameworks.git
   cd rinha-de-python-frameworks
   ```

2. Navigate to the desired framework directory:  
   ```bash
   cd fastapi  # Example for FastAPI
   ```

3. Follow the instructions in the framework's `README.md` to set up and run the project.  

---

## **Rules**  
The goal of this project is to compare and benchmark Python web frameworks by implementing the same API in each framework. The API must adhere to the following rules:  

### **Endpoints**  
Each framework must implement the following endpoints:  

1. **POST /users**  
   - Creates a new person.  
   - Accepts JSON with the following fields:  
     ```json
     {
       "username": "string (required, unique, max 32 chars)",
       "name": "string (required, max 100 chars)",
       "birthdate": "string (required, format: YYYY-MM-DD)",
       "stack": "array of strings (optional, max 32 chars per item)"
     }
     ```
   - Returns:  
     - Status code `201` with the `Location` header pointing to the new resource (`/users/[:id]`).  
     - Status code `422` for invalid data or duplicate `username`.  
     - Status code `400` for syntactically invalid JSON.  

2. **GET /users/[:id]**  
   - Retrieves details of a person by ID.  
   - Returns:  
     - Status code `200` with the person's data in JSON format.  
     - Status code `404` if the person does not exist.  

3. **GET /users?t=[:termo]**  
   - Searches for people by a term (case-insensitive).  
   - The term must be present in `username`, `name`, or `stack`.  
   - Returns:  
     - Status code `200` with a list of matching people (up to 50 results).  
     - Status code `400` if the `t` query parameter is missing.  

4. **GET /count-users**  
   - Returns the total count of people in the database.  
   - This endpoint is not performance-tested.  

---

### **Database**  
- Use **SQLite** as the database for each framework.  
- Persist data to disk (no in-memory databases).  

---

### **Deployment**  
- Each framework must be deployed using **Docker Compose**.  
- The Docker Compose setup must include:  
  - The API instance.  
  - An **Nginx** load balancer.  
  - Resource limits for CPU and memory (e.g., `cpus: '0.25'`, `memory: '0.5GB'`).  

---

### **Testing**  
- Use **[Gatling](https://gatling.io/)** for stress testing.  
- The goal is to evaluate the performance of each framework under load.  

---

## **Contributing**  
Contributions are welcome! Please:  
1. Open an issue to discuss your changes.  
2. Submit a pull request with your implementation.  

---

## **License**  
This project is licensed under the [MIT License](LICENSE).  
