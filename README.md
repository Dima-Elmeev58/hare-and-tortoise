# hare-and-tortoise
class AnimalThread
{
    private string name;
    private int distanceCovered = 0;
    private Random random = new Random();

    public AnimalThread(string name)
    {
        this.name = name;
    }

    public void Run()
    {
        while (distanceCovered < 100)
        {
            int step = random.Next(1, 10); // Шаг от 1 до 9 метров
            distanceCovered += step;

            Console.WriteLine($"{name} пробежал {distanceCovered} метров.");

            // Изменение приоритета, если отстал
            AdjustThreadPriority();

            Thread.Sleep(100); // Задержка для имитации времени на преодоление расстояния
        }

        Console.WriteLine($"{name} достиг 100 метров!");
    }

    private void AdjustThreadPriority()
    {
        var currentThread = Thread.CurrentThread;

        if (distanceCovered < 50)
        {
            currentThread.Priority = ThreadPriority.Highest; // Увеличить приоритет
        }
        else
        {
            currentThread.Priority = ThreadPriority.Normal; // Снизить приоритет
        }
    }
}

class RabbitAndTurtle
{
    public static void Main()
    {
        AnimalThread rabbit = new AnimalThread("Кролик");
        AnimalThread turtle = new AnimalThread("Черепаха");

        // Запуск потоков
        Thread rabbitThread = new Thread(rabbit.Run);
        Thread turtleThread = new Thread(turtle.Run);

        rabbitThread.Start();
        turtleThread.Start();

        // Ожидание завершения потоков
        rabbitThread.Join();
        turtleThread.Join();
    }
}
