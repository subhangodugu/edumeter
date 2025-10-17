// ✅ Corrected import from framer-motion
import { motion } from "framer-motion";
import { Card } from "./ui/card";
import { Button } from "./ui/button";
import { Badge } from "./ui/badge";
import { Input } from "./ui/input";
import { Progress } from "./ui/progress";
import {
    Users, TrendingUp, BookOpen, Building2,
    Search, Plus, Download, MoreVertical
} from "lucide-react";
import {
    BarChart, Bar, LineChart, Line, XAxis, YAxis,
    CartesianGrid, Tooltip, ResponsiveContainer
} from "recharts";

const statsData = [
    { icon: Users, label: "Total Students", value: "2,847", change: "+12%", trend: "up" },
    { icon: BookOpen, label: "Active Assessments", value: "1,234", change: "+8%", trend: "up" },
    { icon: Building2, label: "Partner Institutes", value: "542", change: "+5%", trend: "up" },
    { icon: TrendingUp, label: "Placements", value: "892", change: "+15%", trend: "up" }
];

const chartData = [
    { month: "Jan", students: 400, placements: 240 },
    { month: "Feb", students: 500, placements: 300 },
    { month: "Mar", students: 650, placements: 390 },
    { month: "Apr", students: 720, placements: 432 },
    { month: "May", students: 850, placements: 510 },
    { month: "Jun", students: 980, placements: 588 }
];

const recentStudents = [
    { id: 1, name: "Sarah Johnson", email: "sarah.j@email.com", score: 85, status: "completed", progress: 100 },
    { id: 2, name: "Mike Chen", email: "mike.c@email.com", score: 78, status: "in-progress", progress: 60 },
    { id: 3, name: "Priya Patel", email: "priya.p@email.com", score: 92, status: "completed", progress: 100 },
    { id: 4, name: "James Wilson", email: "james.w@email.com", score: 71, status: "in-progress", progress: 45 },
    { id: 5, name: "Emma Davis", email: "emma.d@email.com", score: 88, status: "completed", progress: 100 }
];

const topCareers = [
    { name: "Software Engineer", count: 342 },
    { name: "Data Scientist", count: 285 },
    { name: "Product Manager", count: 198 },
    { name: "UX Designer", count: 156 },
    { name: "Others", count: 219 }
];

export function DashboardScreen() {
    return (
        <div className="min-h-screen bg-background text-foreground">
            {/* Sidebar */}
            <div className="fixed left-0 top-0 h-screen w-64 bg-card border-r border-border p-6 hidden lg:block">
                <div className="flex items-center gap-2 mb-8">
                    <div className="w-10 h-10 gradient-primary rounded-xl flex items-center justify-center">
                        <TrendingUp className="w-6 h-6 text-white" />
                    </div>
                    <span className="text-xl font-semibold">EduMeter</span>
                </div>

                <nav className="space-y-2">
                    {[
                        { icon: TrendingUp, label: "Dashboard", active: true },
                        { icon: Users, label: "Students" },
                        { icon: BookOpen, label: "Reports" },
                        { icon: Building2, label: "Institutes" }
                    ].map((item, index) => {
                        const Icon = item.icon;
                        return (
                            <button
                                key={index}
                                // ✅ Corrected className syntax with backticks
                                className={`w-full flex items-center gap-3 px-4 py-3 rounded-xl transition-colors ${item.active
                                        ? "gradient-primary text-white"
                                        : "hover:bg-muted text-muted-foreground"
                                    }`}
                            >
                                <Icon className="w-5 h-5" />
                                <span>{item.label}</span>
                            </button>
                        );
                    })}
                </nav>
            </div>

            {/* Main Content */}
            <div className="lg:ml-64 p-6 md:p-8">
                {/* Header */}
                <div className="mb-8">
                    <div className="flex flex-col md:flex-row md:items-center justify-between gap-4 mb-6">
                        <div>
                            <h1 className="mb-1 text-2xl font-semibold">Dashboard</h1>
                            <p className="text-muted-foreground">Welcome back, Admin</p>
                        </div>
                        <div className="flex gap-3">
                            <Button variant="outline" className="rounded-xl">
                                <Download className="w-4 h-4 mr-2" />
                                Export Data
                            </Button>
                            <Button className="gradient-primary text-white rounded-xl">
                                <Plus className="w-4 h-4 mr-2" />
                                Add Institute
                            </Button>
                        </div>
                    </div>

                    {/* Stats Cards */}
                    <div className="grid md:grid-cols-2 lg:grid-cols-4 gap-6">
                        {statsData.map((stat, index) => {
                            const Icon = stat.icon;
                            return (
                                <motion.div
                                    key={index}
                                    initial={{ opacity: 0, y: 20 }}
                                    animate={{ opacity: 1, y: 0 }}
                                    transition={{ delay: index * 0.1 }}
                                >
                                    <Card className="p-6">
                                        <div className="flex items-start justify-between mb-4">
                                            <div className="w-12 h-12 bg-primary/10 rounded-xl flex items-center justify-center">
                                                <Icon className="w-6 h-6 text-primary" />
                                            </div>
                                            <Badge
                                                variant="outline"
                                                // Corrected className syntax with backticks
                                                className={`${stat.trend === "up"
                                                        ? "text-secondary border-secondary/50"
                                                        : "text-destructive border-destructive/50"
                                                    }`}
                                            >
                                                {stat.change}
                                            </Badge>
                                        </div>
                                        <div className="text-3xl font-semibold mb-1">{stat.value}</div>
                                        <div className="text-sm text-muted-foreground">{stat.label}</div>
                                    </Card>
                                </motion.div>
                            );
                        })}
                    </div>
                </div>

                {/* Charts */}
                <div className="grid lg:grid-cols-2 gap-6 mb-8">
                    {/* Growth Chart */}
                    <motion.div
                        initial={{ opacity: 0, y: 20 }}
                        animate={{ opacity: 1, y: 0 }}
                        transition={{ delay: 0.4 }}
                    >
                        <Card className="p-6">
                            <h3 className="mb-6 font-semibold">Student Growth & Placements</h3>
                            <ResponsiveContainer width="100%" height={300}>
                                <LineChart data={chartData}>
                                    <CartesianGrid strokeDasharray="3 3" stroke="rgba(0,0,0,0.05)" />
                                    <XAxis dataKey="month" />
                                    <YAxis />
                                    <Tooltip />
                                    <Line type="monotone" dataKey="students" stroke="#4F46E5" strokeWidth={2} dot />
                                    <Line type="monotone" dataKey="placements" stroke="#22C55E" strokeWidth={2} dot />
                                </LineChart>
                            </ResponsiveContainer>
                        </Card>
                    </motion.div>

                    {/* Career Distribution */}
                    <motion.div
                        initial={{ opacity: 0, y: 20 }}
                        animate={{ opacity: 1, y: 0 }}
                        transition={{ delay: 0.5 }}
                    >
                        <Card className="p-6">
                            <h3 className="mb-6 font-semibold">Top Career Choices</h3>
                            <ResponsiveContainer width="100%" height={300}>
                                <BarChart data={topCareers}>
                                    <CartesianGrid strokeDasharray="3 3" stroke="rgba(0,0,0,0.05)" />
                                    <XAxis dataKey="name" angle={-45} textAnchor="end" height={100} />
                                    <YAxis />
                                    <Tooltip />
                                    <Bar dataKey="count" fill="#4F46E5" radius={[8, 8, 0, 0]} />
                                </BarChart>
                            </ResponsiveContainer>
                        </Card>
                    </motion.div>
                </div>

                {/* Students Table */}
                <motion.div
                    initial={{ opacity: 0, y: 20 }}
                    animate={{ opacity: 1, y: 0 }}
                    transition={{ delay: 0.6 }}
                >
                    <Card className="p-6">
                        <div className="flex flex-col md:flex-row md:items-center justify-between gap-4 mb-6">
                            <h3 className="font-semibold">Recent Students</h3>
                            <div className="relative">
                                <Search className="absolute left-3 top-1/2 -translate-y-1/2 w-4 h-4 text-muted-foreground" />
                                <Input placeholder="Search students..." className="pl-10 rounded-xl" />
                            </div>
                        </div>

                        <div className="overflow-x-auto">
                            <table className="w-full min-w-[640px]">
                                <thead>
                                    <tr className="border-b border-border text-left">
                                        <th className="pb-3 text-sm font-medium text-muted-foreground">Student</th>
                                        <th className="pb-3 text-sm font-medium text-muted-foreground">Email</th>
                                        <th className="pb-3 text-sm font-medium text-muted-foreground">Score</th>
                                        <th className="pb-3 text-sm font-medium text-muted-foreground">Progress</th>
                                        <th className="pb-3 text-sm font-medium text-muted-foreground">Status</th>
                                        <th className="pb-3 text-sm font-medium text-muted-foreground"></th>
                                    </tr>
                                </thead>
                                <tbody>
                                    {recentStudents.map((student) => (
                                        <tr key={student.id} className="border-b border-border last:border-0">
                                            <td className="py-4 font-medium">{student.name}</td>
                                            <td className="py-4 text-muted-foreground">{student.email}</td>
                                            <td className="py-4">
                                                <Badge className="gradient-primary text-white border-0">
                                                    {student.score}
                                                </Badge>
                                            </td>
                                            <td className="py-4">
                                                <div className="flex items-center gap-2">
                                                    <Progress value={student.progress} className="h-2 w-24" />
                                                    <span className="text-sm text-muted-foreground">
                                                        {student.progress}%
                                                    </span>
                                                </div>
                                            </td>
                                            <td className="py-4">
                                                <Badge
                                                    variant={student.status === "completed" ? "default" : "outline"}
                                                >
                                                    {student.status}
                                                </Badge>
                                            </td>
                                            <td className="py-4">
                                                <Button variant="ghost" size="icon" className="rounded-lg">
                                                    <MoreVertical className="w-4 h-4" />
                                                </Button>
                                            </td>
                                        </tr>
                                    ))}
                                </tbody>
                            </table>
                        </div>
                    </Card>
                </motion.div>
            </div>
        </div>
    );
}
