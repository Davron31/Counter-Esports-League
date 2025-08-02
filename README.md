import React, { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Tabs, TabsContent, TabsList, TabsTrigger } from "@/components/ui/tabs";
import { motion } from "framer-motion";
import { Trophy, LayoutGrid, Settings, X, Pencil } from "lucide-react";

const STATUS_COLORS = {
  Прошедший: "bg-red-500",
  Активный: "bg-green-500",
  Предстоящий: "bg-gray-500"
};

export default function CounterEsportsLeague() {
  const [selectedTournament, setSelectedTournament] = useState(null);
  const [participants, setParticipants] = useState({});
  const [newTournament, setNewTournament] = useState("");
  const [newTeam, setNewTeam] = useState({ name: "", logo: "" });
  const [statuses, setStatuses] = useState({});
  const [newStatus, setNewStatus] = useState("Предстоящий");

  const handleAddTournament = () => {
    if (newTournament && !participants[newTournament]) {
      setParticipants({ ...participants, [newTournament]: [] });
      setStatuses({ ...statuses, [newTournament]: newStatus });
      setNewTournament("");
      setNewStatus("Предстоящий");
    }
  };

  const handleDeleteTournament = (title) => {
    const { [title]: _, ...rest } = participants;
    const { [title]: __, ...restStatus } = statuses;
    setParticipants(rest);
    setStatuses(restStatus);
    if (selectedTournament === title) setSelectedTournament(null);
  };

  const handleAddTeam = () => {
    if (selectedTournament && newTeam.name && newTeam.logo) {
      setParticipants({
        ...participants,
        [selectedTournament]: [...participants[selectedTournament], newTeam]
      });
      setNewTeam({ name: "", logo: "" });
    }
  };

  const handleChangeStatus = (title, newStatus) => {
    setStatuses({ ...statuses, [title]: newStatus });
  };

  return (
    <main className="min-h-screen bg-gradient-to-b from-gray-800 to-gray-900 text-gray-100 p-4">
      <header className="text-center py-8">
        <motion.h1
          initial={{ opacity: 0, y: -20 }}
          animate={{ opacity: 1, y: 0 }}
          transition={{ duration: 0.8 }}
          className="text-4xl font-bold"
        >
          Counter Esports League
        </motion.h1>
      </header>

      <Tabs defaultValue="tournaments" className="w-full max-w-5xl mx-auto">
        <TabsList className="grid grid-cols-3 gap-2">
          <TabsTrigger value="tournaments" className="flex items-center gap-2">
            <Trophy className="w-4 h-4" />Турниры
          </TabsTrigger>
          <TabsTrigger value="bracket" className="flex items-center gap-2">
            <LayoutGrid className="w-4 h-4" />Сетка
          </TabsTrigger>
          <TabsTrigger value="admin" className="flex items-center gap-2">
            <Settings className="w-4 h-4" />Админ панель
          </TabsTrigger>
        </TabsList>

        <TabsContent value="tournaments">
          <motion.div
            initial={{ opacity: 0, y: 10 }}
            animate={{ opacity: 1, y: 0 }}
            transition={{ duration: 0.6 }}
            className="grid grid-cols-1 md:grid-cols-2 gap-4 mt-6"
          >
            {Object.keys(participants).map((title, index) => (
              <Card key={index} className="bg-white rounded-2xl shadow-md text-gray-900">
                <CardContent className="p-4 relative">
                  <div className="absolute top-3 right-3 flex gap-2">
                    <select
                      className="text-xs p-1 border rounded"
                      value={statuses[title] || "Предстоящий"}
                      onChange={(e) => handleChangeStatus(title, e.target.value)}
                    >
                      <option value="Предстоящий">Предстоящий</option>
                      <option value="Активный">Активный</option>
                      <option value="Прошедший">Прошедший</option>
                    </select>
                    <X className="w-4 h-4 text-gray-500 hover:text-red-500 cursor-pointer" onClick={() => handleDeleteTournament(title)} />
                  </div>
                  <h2 className="text-xl font-semibold mb-1 flex items-center gap-2">
                    <span
                      className={`w-3 h-3 rounded-full ${STATUS_COLORS[statuses[title] || "Предстоящий"]}`}
                    ></span>
                    {title}
                  </h2>
                  <p className="text-sm text-gray-600">Статус: {statuses[title] || "Предстоящий"}</p>
                  <Button className="mt-4" onClick={() => setSelectedTournament(title)}>
                    Подробнее
                  </Button>
                </CardContent>
              </Card>
            ))}
          </motion.div>

          {selectedTournament && (
            <motion.div
              initial={{ opacity: 0, y: 20 }}
              animate={{ opacity: 1, y: 0 }}
              transition={{ duration: 0.5 }}
              className="bg-white rounded-2xl shadow-xl p-6 mt-8 text-gray-900"
            >
              <h3 className="text-2xl font-semibold mb-4">
                Участники: {selectedTournament}
              </h3>
              <ul className="grid grid-cols-1 sm:grid-cols-2 gap-4">
                {participants[selectedTournament].map((team, i) => (
                  <li key={i} className="flex items-center gap-4 p-2 border rounded-lg">
                    <img src={team.logo} alt={team.name} className="w-10 h-10 object-contain" />
                    <span className="font-medium">{team.name}</span>
                  </li>
                ))}
              </ul>
              <div className="mt-6 space-y-2">
                <input
                  type="text"
                  placeholder="Название команды"
                  className="w-full p-2 border rounded-lg"
                  value={newTeam.name}
                  onChange={(e) => setNewTeam({ ...newTeam, name: e.target.value })}
                />
                <input
                  type="text"
                  placeholder="Ссылка на логотип"
                  className="w-full p-2 border rounded-lg"
                  value={newTeam.logo}
                  onChange={(e) => setNewTeam({ ...newTeam, logo: e.target.value })}
                />
                <Button onClick={handleAddTeam}>Добавить команду</Button>
              </div>
              <Button className="mt-4" onClick={() => setSelectedTournament(null)}>
                Закрыть
              </Button>
            </motion.div>
          )}
        </TabsContent>

        <TabsContent value="bracket">
          <motion.div
            initial={{ opacity: 0, scale: 0.95 }}
            animate={{ opacity: 1, scale: 1 }}
            transition={{ duration: 0.5 }}
            className="bg-white rounded-2xl shadow-lg p-6 mt-6 text-center text-gray-900"
          >
            <h2 className="text-2xl font-bold mb-4">Турнирная сетка</h2>
            <p className="text-gray-500">Здесь будет визуализация сетки турнира (coming soon).</p>
          </motion.div>
        </TabsContent>

        <TabsContent value="admin">
          <motion.div
            initial={{ opacity: 0, x: 20 }}
            animate={{ opacity: 1, x: 0 }}
            transition={{ duration: 0.4 }}
            className="bg-white rounded-2xl shadow-lg p-6 mt-6 text-gray-900"
          >
            <h2 className="text-2xl font-semibold mb-4">Админ панель</h2>
            <div className="space-y-4">
              <input
                type="text"
                placeholder="Название турнира"
                className="w-full p-2 border rounded-lg"
                value={newTournament}
                onChange={(e) => setNewTournament(e.target.value)}
              />
              <select
                className="w-full p-2 border rounded-lg"
                value={newStatus}
                onChange={(e) => setNewStatus(e.target.value)}
              >
                <option value="Предстоящий">Предстоящий</option>
                <option value="Активный">Активный</option>
                <option value="Прошедший">Прошедший</option>
              </select>
              <Button onClick={handleAddTournament}>Добавить турнир</Button>
            </div>
          </motion.div>
        </TabsContent>
      </Tabs>
    </main>
  );
}
