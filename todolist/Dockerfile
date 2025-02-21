# Use an official Python runtime as a base image
FROM python:3.13

# Set the working directory inside the container
WORKDIR /app

# Copy the requirements.txt file and install dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy the rest of the application code
COPY . .
# Copy the .env file
COPY .env .env
# Set environment variables
ENV DJANGO_SETTINGS_MODULE=todolist.settings
# Copy the SQLite database to persist data
COPY db.sqlite3 /app/db.sqlite3


# Run collectstatic
RUN export $(cat .env | xargs) && python manage.py collectstatic --noinput

# Expose port 8000 (same as Django’s default)
EXPOSE 8000

# Run the application using Waitress
CMD ["waitress-serve", "--listen=0.0.0.0:8000", "todolist.wsgi:application"]
