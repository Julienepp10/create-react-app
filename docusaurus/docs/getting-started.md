
import React, { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { motion } from "framer-motion";

const articles = [
  {
    title: "Le Tournoi des 6 Nations : Résumé de la dernière journée",
    content: "Le Tournoi des 6 Nations est l'un des événements les plus prestigieux du rugby mondial. Lors de la dernière journée, l'équipe de France a réalisé une performance exceptionnelle contre l'Angleterre, avec des essais spectaculaires et un jeu dynamique.",
    image: "/images/tournoi6nations.jpg", // Assurez-vous de télécharger l'image correspondante dans le dossier public/images
    video: "https://www.youtube.com/embed/xyz1", // Remplacez par un vrai lien YouTube
    date: "2025-03-20",
    author: "Jean Dupont",
    category: "Tournois"
  },
  {
    title: "Top 14 : Analyse de la saison en cours",
    content: "Cette saison du Top 14 est pleine de surprises. Plusieurs équipes sont en forme, tandis que d'autres ont du mal à trouver leur rythme. On analyse les performances des joueurs clés et les équipes à suivre.",
    image: "/images/top14.jpg", // Assurez-vous de télécharger l'image correspondante dans le dossier public/images
    video: "https://www.youtube.com/embed/xyz2", // Remplacez par un vrai lien YouTube
    date: "2025-03-19",
    author: "Marie Lefevre",
    category: "Championnat National"
  },
  {
    title: "Coupe du Monde 2027 : Ce qu'il faut savoir",
    content: "La Coupe du Monde 2027 se prépare activement. Les équipes se qualifient, les stades sont en construction, et de nouvelles règles seront appliquées. Découvrez tout ce qu'il faut savoir sur cette compétition mondiale.",
    image: "/images/coupe2027.jpg", // Assurez-vous de télécharger l'image correspondante dans le dossier public/images
    video: "https://www.youtube.com/embed/xyz3", // Remplacez par un vrai lien YouTube
    date: "2025-03-18",
    author: "Pierre Martin",
    category: "Compétitions Internationales"
  }
];

const liveUpdates = [
  "Essai spectaculaire de l'équipe de France contre l'Angleterre!",
  "Le Stade Toulousain recrute un nouveau joueur clé pour la saison prochaine.",
  "Les nouvelles règles du rugby expliquées en détail."
];

export default function RugbyNews() {
  const [comments, setComments] = useState([]);
  const [newComment, setNewComment] = useState("");
  const [selectedArticle, setSelectedArticle] = useState(null);

  const handleCommentSubmit = () => {
    if (newComment.trim() !== "") {
      setComments([...comments, newComment]);
      setNewComment("");
    }
  };

  if (selectedArticle) {
    return (
      <div className="p-6 bg-gray-100 min-h-screen">
        <Button onClick={() => setSelectedArticle(null)} className="mb-4">Retour</Button>
        <Card className="shadow-lg rounded-2xl overflow-hidden">
          <CardContent className="p-4">
            <img src={selectedArticle.image} alt={selectedArticle.title} className="w-full h-60 object-cover rounded-lg mb-4" />
            <h2 className="text-2xl font-semibold">{selectedArticle.title}</h2>
            <p className="text-gray-600 mt-2">{selectedArticle.content}</p>
            <p className="text-gray-500 mt-2 text-sm">Publié le {selectedArticle.date} par {selectedArticle.author} - Catégorie: {selectedArticle.category}</p>
            <div className="mt-4">
              <iframe 
                width="100%" 
                height="300" 
                src={selectedArticle.video} 
                title={selectedArticle.title} 
                frameBorder="0" 
                allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" 
                allowFullScreen
              ></iframe>
            </div>
          </CardContent>
        </Card>
      </div>
    );
  }

  return (
    <div className="p-6 bg-gray-100 min-h-screen">
      <h1 className="text-3xl font-bold text-center mb-6">Actualités Rugby</h1>
      
      {/* Fil d'actualités en direct */}
      <div className="bg-white p-4 rounded-lg shadow mb-6">
        <h2 className="text-2xl font-semibold mb-2">Fil d'actualités en direct</h2>
        <ul className="list-disc pl-5 text-gray-700">
          {liveUpdates.map((update, index) => (
            <li key={index} className="mb-1">{update}</li>
          ))}
        </ul>
      </div>
      
      <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
        {articles.map((article, index) => (
          <motion.div
            key={index}
            whileHover={{ scale: 1.05 }}
            className="cursor-pointer"
            onClick={() => setSelectedArticle(article)}
          >
            <Card className="shadow-lg rounded-2xl overflow-hidden">
              <CardContent className="p-4">
                <img src={article.image} alt={article.title} className="w-full h-40 object-cover rounded-lg mb-4" />
                <h2 className="text-xl font-semibold">{article.title}</h2>
                <p className="text-gray-600 mt-2">{article.content}</p>
                <p className="text-gray-500 mt-2 text-sm">Publié le {article.date} par {article.author} - Catégorie: {article.category}</p>
                <Button className="mt-4">Lire plus</Button>
              </CardContent>
            </Card>
          </motion.div>
        ))}
      </div>

      {/* Section commentaires */}
      <div className="bg-white p-4 rounded-lg shadow mt-6">
        <h2 className="text-2xl font-semibold mb-2">Commentaires</h2>
        <div className="mb-4">
          <input 
            type="text" 
            className="w-full p-2 border rounded-lg" 
            placeholder="Ajoutez un commentaire..." 
            value={newComment} 
            onChange={(e) => setNewComment(e.target.value)}
          />
          <Button className="mt-2" onClick={handleCommentSubmit}>Envoyer</Button>
        </div>
        <ul className="list-disc pl-5 text-gray-700">
          {comments.map((comment, index) => (
            <li key={index} className="mb-1">{comment}</li>
          ))}
        </ul>
      </div>
    </div>
  );
}
