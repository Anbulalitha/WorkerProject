# WorkerProject
This project is a  WorkerProject built using ASP.NET and  MVC. It includes both frontend and backend components. The backend is developed with ASP.NET, and the frontend is managed using a modern JavaScript framework. This README file provides instructions for setting up the project, including package installation, model creation, migrations, and controller function implementations.

Table of contents:
=>Getting Started
=>Prerequisites
=>Installation
=>Backend Setup
=>Package Installation
=>Creating Models
=>Migrations
=>Controller Functions
=>Frontend Setup
=>Running the Application

Creating Models:
namespace WorkerManagementSystem.Models
{
    public class Worker
    {
        public int WorkerID { get; set; }
        public string WorkerName { get; set; }
        public string Category { get; set; }
        public string Location { get; set; }
    }
}

Migrations:
Add migrations and update the database:

sh
dotnet ef migrations add InitialCreate
dotnet ef database update


Controller Functions
Create a controller to handle CRUD operations. Here's an example for the Worker controller:

using WorkerManagementSystem.Models;
using Microsoft.AspNetCore.Mvc;
using System.Linq;

namespace WorkerManagementSystem.Controllers
{
    public class WorkerController : Controller
    {
        private readonly WorkerContext _context;

        public WorkerController(WorkerContext context)
        {
            _context = context;
        }

        public IActionResult Index()
        {
            return View(_context.Workers.ToList());
        }

        [HttpGet]
        public IActionResult AddWorker()
        {
            return View();
        }

        [HttpPost]
        public IActionResult AddWorker(Worker worker)
        {
            if (ModelState.IsValid)
            {
                _context.Workers.Add(worker);
                _context.SaveChanges();
                return RedirectToAction("Index");
            }
            return View(worker);
        }

        public IActionResult Details(int id)
        {
            var worker = _context.Workers.Find(id);
            if (worker == null)
            {
                return NotFound();
            }
            return View(worker);
        }
    }
}


