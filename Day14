internal class Program
{
    private static void Main()
    {
        string[] input = File.ReadAllLines(@"C:\Users\Will\source\repos\AoC 2022\AoC2022\Input Data\Day14.txt");
        Dictionary<(int, int), string> grid = new();
        int deepest = 0;
        int[] start = new int[] { 500, 0 };
        // Build Walls

        foreach (string line in input)
        {
            string[] coords = line.Split("->").Select(x => x.Trim()).ToArray();


            for (int i = 0; i < coords.Length - 1; i++)
            {
                int[] pt1 = coords[i].Split(',').Select(x => int.Parse(x)).ToArray();
                int[] pt2 = coords[i + 1].Split(',').Select(x => int.Parse(x)).ToArray();
                deepest = Math.Max(deepest, Math.Max(pt1[1], pt2[1]));

                if (pt1[0] == pt2[0]) // x cord the same
                {
                    int max = Math.Max(pt1[1], pt2[1]);
                    int min = Math.Min(pt1[1], pt2[1]);

                    for (int x = min; x <= max; x++)
                    {
                        try { grid.Add((pt1[0], x), "#"); } catch { }
                    }
                }
                else
                {
                    int max = Math.Max(pt1[0], pt2[0]);
                    int min = Math.Min(pt1[0], pt2[0]);

                    for (int x = min; x <= max; x++)
                    {
                        try { grid.Add((x, pt1[1]), "#"); } catch { }
                    }
                }
            }
        }

        int left = 500 - (deepest + 2);
        int right = 500 + (deepest + 2);

        for (int x = left; x <= right; x++)
        {
            grid.Add((x, deepest + 2), "#");
        }
        //start falling sand
        int grainCount = 0;
        bool overflow = false;

        while (overflow == false)
        {
            int[] newGrain = { 500, 0 };
            bool grainMoving = true;
            while (grainMoving == true)
            {

                if (grid.ContainsKey((newGrain[0], newGrain[1] + 1)) != true) //if no wall below = move down
                {
                    newGrain[1]++;

                }
                else if (grid.ContainsKey((newGrain[0] - 1, newGrain[1] + 1)) != true) // if wall below and no wall bottom left = move there
                {
                    newGrain[1]++;
                    newGrain[0]--;
                }
                else if (grid.ContainsKey((newGrain[0] + 1, newGrain[1] + 1)) != true) // if wall below and left = move right
                {
                    newGrain[1]++;
                    newGrain[0]++;
                }
                else                //come to stop
                {
                    grid.Add((newGrain[0], newGrain[1]), "o");
                    grainMoving = false;
                    grainCount++;
                }
                if (grid.ContainsKey((500, 0))) { overflow = true; grainMoving = false; }

            }
        }
        Console.WriteLine(grainCount);
    }
}
