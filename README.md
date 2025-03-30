# TD
برای برانامه ریزی روزانه
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.git
git push -u origin main

import { useState } from "reacimport { Button } from "@/components/ui/button";
import { Card, CardContent } from "@/components/ui/card";
import { Select, SelectItem } from "@/components/ui/select";
import { Checkbox } from "@/components/ui/checkbox";
import { Textarea } from "@/components/ui/textarea";
import { motion } from "framer-motion";

const colors = [
  "red", "blue", "green", "yellow", "purple", "orange", "pink",
  "brown", "gray", "cyan", "lime", "indigo", "teal", "olive", "navy",
  "maroon", "gold", "silver", "black", "white", "violet", "magenta", "coral",
  "salmon", "khaki", "plum", "orchid", "turquoise", "lavender", "beige"
];

export default function DailyPlanner() {
  const [bgColor, setBgColor] = useState("white");
  const [tasks, setTasks] = useState({});
  const [completedTasks, setCompletedTasks] = useState({});
  const [day, setDay] = useState("Monday");

  const handleTaskChange = (e) => {
    setTasks({ ...tasks, [day]: e.target.value });
  };

  const toggleTaskCompletion = () => {
    setCompletedTasks({ ...completedTasks, [day]: !completedTasks[day] });
  };

  const generatePlan = async () => {
    const response = await fetch("https://api.openai.com/v1/completions", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        "Authorization": `Bearer YOUR_OPENAI_API_KEY`
      },
      body: JSON.stringify({
        model: "gpt-4",
        prompt: `یک برنامه روزانه برای ${day} پیشنهاد بده که شامل کارهای مفید باشد.`,
        max_tokens: 100
      })
    });
    const data = await response.json();
    setTasks({ ...tasks, [day]: data.choices[0].text });
  };

  return (
    <motion.div className="min-h-screen flex flex-col items-center p-6" animate={{ backgroundColor: bgColor }}>
      <h1 className="text-3xl font-bold mb-4">برنامه روزانه</h1>
      <Select value={day} onChange={setDay} className="mb-4">
        {["Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"].map(d => (
          <SelectItem key={d} value={d}>{d}</SelectItem>
        ))}
      </Select>
      <Select value={bgColor} onChange={setBgColor} className="mb-4">
        {colors.map(color => (
          <SelectItem key={color} value={color}>{color}</SelectItem>
        ))}
      </Select>
      <Card className="w-full max-w-md p-4">
        <CardContent>
          <Textarea value={tasks[day] || ""} onChange={handleTaskChange} placeholder="برنامه خود را وارد کنید" />
          <div className="flex items-center mt-2">
            <Checkbox checked={completedTasks[day] || false} onCheckedChange={toggleTaskCompletion} />
            <span className="ml-2">انجام شد</span>
          </div>
          <Button onClick={generatePlan} className="mt-4">برنامه پیشنهادی</Button>
        </CardContent>
      </Card>
    </motion.div>
  );
}
