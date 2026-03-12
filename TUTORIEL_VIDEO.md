Tutoriel : Créer la vidéo promotionnelle Content-SEO.ai avec Remotion

> **🎯 Objectif de la mission :** > Créer une vidéo promotionnelle de 15 secondes entièrement codée en React à l'aide de la librairie **Remotion**. Cette vidéo sera utilisée sur la Landing Page de notre SaaS pour présenter notre outil d'IA et inciter les utilisateurs à s'abonner.

## 🛠️ Prérequis
Avant de commencer, assurez-vous d'avoir installé sur votre machine :
* **Node.js** (version 16 ou supérieure).
* Un éditeur de code (VS Code recommandé).
* Un terminal prêt à l'emploi.

---

## Étape 1 : Initialiser le projet Remotion

Nous allons créer un projet isolé pour la vidéo afin de ne pas mélanger les dépendances avec le projet web principal.

1. Ouvrez votre terminal et placez-vous dans le dossier de votre choix.
2. Lancez la commande suivante pour créer le projet :
   
   npx create-remotion@latest video-content-seo

Le terminal va vous poser quelques questions. Choisissez le template Blank (projet vide en TypeScript/React).

Entrez dans le dossier du projet et installez les dépendances :


cd video-content-seo
npm install
Étape 2 : Créer la scène de la vidéo
Dans un projet Remotion, les vidéos sont de simples composants React (.tsx).

Allez dans le dossier src/.

Créez un nouveau fichier nommé PromoVideo.tsx.

Copiez-collez le code complet suivant dans ce fichier :

TypeScript
import { AbsoluteFill, interpolate, Sequence, useCurrentFrame, useVideoConfig, spring } from 'remotion';
import React from 'react';

// --- CONFIGURATION DE LA CHARTE GRAPHIQUE ---
const THEME = {
  bg: '#0F172A',       
  primary: '#3B82F6',  
  accent: '#8B5CF6',   
  text: '#F8FAFC',     
  window: '#FFFFFF',   
};

// --- SCÈNE 1 : LE LOGO (0s à 3.3s) ---
const LogoScene = () => {
  const frame = useCurrentFrame();
  const { fps } = useVideoConfig();
  const scale = spring({ frame, fps, from: 0.5, to: 1, config: { damping: 10 } });
  const opacity = interpolate(frame, [0, 20], [0, 1]);

  return (
    <AbsoluteFill style={{ backgroundColor: THEME.bg, justifyContent: 'center', alignItems: 'center' }}>
      <div style={{ transform: `scale(${scale})`, opacity, textAlign: 'center' }}>
        <h1 style={{ fontFamily: 'sans-serif', fontSize: 90, fontWeight: 900, color: THEME.text, margin: 0 }}>
          Content-SEO<span style={{ color: THEME.primary }}>.ai</span>
        </h1>
        <p style={{ fontFamily: 'sans-serif', fontSize: 32, color: '#94A3B8', marginTop: 10 }}>
          Rankez plus haut, plus vite.
        </p>
      </div>
    </AbsoluteFill>
  );
};

// --- SCÈNE 2 : DEMO DASHBOARD (3.3s à 11s) ---
const DashboardScene = () => {
  const frame = useCurrentFrame();
  const { fps } = useVideoConfig();

  const windowSlide = spring({ frame, fps, from: 100, to: 0, config: { stiffness: 50 } });
  const windowOpacity = interpolate(frame, [0, 20], [0, 1]);

  const text = "Génération de l'article optimisé SEO pour 'SaaS Marketing'...";
  const chars = Math.round(interpolate(frame, [40, 100], [0, text.length], { extrapolateRight: 'clamp' }));
  const cursor = Math.floor(frame / 10) % 2 === 0 ? '|' : '';

  return (
    <AbsoluteFill style={{ backgroundColor: THEME.bg, alignItems: 'center', justifyContent: 'center' }}>
      <div style={{
        width: 1400, height: 800, backgroundColor: THEME.window, borderRadius: 20,
        boxShadow: '0 50px 100px -20px rgba(0,0,0,0.6)', overflow: 'hidden',
        transform: `translateY(${windowSlide}px)`, opacity: windowOpacity,
        display: 'flex', flexDirection: 'column'
      }}>
        <div style={{ height: 60, backgroundColor: '#F1F5F9', borderBottom: '1px solid #E2E8F0', display: 'flex', alignItems: 'center', padding: '0 20px', gap: 15 }}>
          <div style={{ display: 'flex', gap: 8 }}>
             <div style={{ width: 14, height: 14, borderRadius: '50%', backgroundColor: '#EF4444' }}/>
             <div style={{ width: 14, height: 14, borderRadius: '50%', backgroundColor: '#F59E0B' }}/>
             <div style={{ width: 14, height: 14, borderRadius: '50%', backgroundColor: '#10B981' }}/>
          </div>
          <div style={{ flex: 1, backgroundColor: 'white', height: 36, borderRadius: 8, display: 'flex', alignItems: 'center', paddingLeft: 15, fontSize: 14, color: '#64748B', border: '1px solid #E2E8F0', fontFamily: 'monospace' }}>
            [https://content-seo.ai/dashboard](https://content-seo.ai/dashboard)
          </div>
        </div>

        <div style={{ flex: 1, padding: 50, display: 'flex', gap: 40, fontFamily: 'sans-serif' }}>
          <div style={{ width: 250, backgroundColor: '#F8FAFC', borderRadius: 12 }}></div>
          <div style={{ flex: 1 }}>
            <h2 style={{ fontSize: 32, color: '#1E293B', marginBottom: 20 }}>Générateur IA</h2>
            <div style={{ 
              padding: 30, backgroundColor: '#F5F3FF', border: `2px solid ${THEME.accent}`, 
              borderRadius: 12, color: THEME.accent, fontSize: 24, fontFamily: 'monospace', minHeight: 100
            }}>
              {text.slice(0, chars)}{cursor}
            </div>
            <div style={{ display: 'flex', gap: 20, marginTop: 30 }}>
               {[1, 2, 3].map((i) => (
                 <div key={i} style={{ 
                   height: 120, flex: 1, backgroundColor: 'white', border: '1px solid #E2E8F0', borderRadius: 12,
                   opacity: interpolate(frame, [100 + (i * 10), 120 + (i * 10)], [0, 1]),
                   transform: `translateY(${interpolate(frame, [100 + (i * 10), 120 + (i * 10)], [20, 0])}px)`
                 }} />
               ))}
            </div>
          </div>
        </div>
      </div>
    </AbsoluteFill>
  );
};

// --- SCÈNE 3 : CALL TO ACTION (11s à 15s) ---
const CTAScene = () => {
  const frame = useCurrentFrame();
  const { fps } = useVideoConfig();
  const scale = spring({ frame, fps, from: 0.8, to: 1, config: { stiffness: 120 } });

  return (
    <AbsoluteFill style={{ backgroundColor: THEME.primary, justifyContent: 'center', alignItems: 'center' }}>
      <div style={{ transform: `scale(${scale})`, textAlign: 'center', color: 'white', fontFamily: 'sans-serif' }}>
        <h2 style={{ fontSize: 70, fontWeight: 900, marginBottom: 10 }}>Essayez l'IA gratuitement.</h2>
        <div style={{ fontSize: 30, opacity: 0.9 }}>Rejoignez-nous sur</div>
        <div style={{ 
          marginTop: 40, backgroundColor: 'white', color: THEME.primary, 
          padding: '20px 60px', borderRadius: 100, fontSize: 40, fontWeight: 'bold'
        }}>
          content-seo.ai
        </div>
      </div>
    </AbsoluteFill>
  );
};

// --- COMPOSITION PRINCIPALE ---
export const MyVideo = () => {
  return (
    <AbsoluteFill style={{ backgroundColor: 'black' }}>
      <Sequence from={0} durationInFrames={100}>
        <LogoScene />
      </Sequence>
      <Sequence from={100} durationInFrames={230}>
        <DashboardScene />
      </Sequence>
      <Sequence from={330} durationInFrames={120}>
        <CTAScene />
      </Sequence>
    </AbsoluteFill>
  );
};
Étape 3 : Enregistrer la vidéo dans Remotion
Ouvrez le fichier src/Root.tsx (ou src/index.ts).

Remplacez le contenu par ceci :

TypeScript
import { Composition } from 'remotion';
import { MyVideo } from './PromoVideo';
import React from 'react';

export const RemotionRoot: React.FC = () => {
  return (
    <>
      <Composition
        id="PromoContentSEO"
        component={MyVideo}
        durationInFrames={450} 
        fps={30}
        width={1920}
        height={1080}
      />
    </>
  );
};
Étape 4 : Prévisualiser le résultat (Le Studio)
Dans le terminal, lancez la commande :


npm start
Votre navigateur va s'ouvrir sur http://localhost:3000.

Cliquez sur "Play" ou appuyez sur Espace pour voir l'animation se jouer !

Étape 5 : Exporter la vidéo finale en MP4
Arrêtez le serveur (Ctrl + C dans le terminal).

Lancez la commande de rendu :


npx remotion render src/index.ts PromoContentSEO out/video-finale.mp4
Le fichier video-finale.mp4 va être généré dans le dossier out/.

Étape 6 : Intégration sur la Landing Page
Placez le fichier .mp4 généré dans le dossier public de votre projet web principal et utilisez ce code pour l'afficher :

JavaScript
<video 
  src="/video-finale.mp4" 
  autoPlay 
  loop 
  muted 
  playsInline
  style={{ width: '100%', borderRadius: '16px', boxShadow: '0 20px 40px rgba(0,0,0,0.2)' }}
/>

--------------------------------------------------

INTEGRATION ET ANIMATION DU LOGO NEOTECHRAMS

L'importation : On importe Img et staticFile depuis remotion.

staticFile() : Cette fonction dit à Remotion : "Va chercher ce fichier dans le dossier public, que ce soit pendant la prévisualisation dans le Studio ou lors du rendu final".

Ajustement de la taille : Les stagiaires devront modifier la valeur width: '400px' dans le style de l'image pour l'adapter aux proportions exactes de votre logo.

Intégration dans le Navbar (Optionnel mais recommandé)
Puisque nous avons simulé une interface de navigateur dans la scène 2 (DashboardScene), il serait aussi très pertinent de remplacer le faux texte "Logo" en haut à gauche de la fausse interface par une version plus petite du vrai logo.

Dans DashboardScene, ils peuvent remplacer le texte brut par :

TypeScript
{/* Remplacez un simple <div>Logo</div> par ceci : */}
<Img 
  src={staticFile("logo-content-seo.svg")} 
  style={{ height: '30px', width: 'auto' }} // Taille adaptée pour une navbar
/>



Le Code Mis à Jour (La Scène du Logo)

Voici comment modifier la LogoScene dans le fichier PromoVideo.tsx pour remplacer le texte par l'image du logo, tout en gardant l'animation de zoom (scale) et d'apparition (opacity).

import { 
  AbsoluteFill, 
  interpolate, 
  useCurrentFrame, 
  useVideoConfig, 
  spring, 
  Img, // <-- 1. Importer Img
  staticFile // <-- 2. Importer staticFile
} from 'remotion';
import React from 'react';

// ... (le reste de ta configuration THEME) ...

// --- SCÈNE 1 : LE LOGO ANIMÉ (Mise à jour) ---
const LogoScene = () => {
  const frame = useCurrentFrame();
  const { fps } = useVideoConfig();
  
  // Animation : Le logo zoome légèrement et apparaît
  const scale = spring({ frame, fps, from: 0.5, to: 1, config: { damping: 10 } });
  const opacity = interpolate(frame, [0, 20], [0, 1]);

  return (
    <AbsoluteFill style={{ backgroundColor: THEME.bg, justifyContent: 'center', alignItems: 'center' }}>
      <div style={{ transform: `scale(${scale})`, opacity, textAlign: 'center', display: 'flex', flexDirection: 'column', alignItems: 'center' }}>
        
        {/* L'IMAGE DU LOGO */}
        <Img 
          src={staticFile("logo-content-seo.svg")} // <-- 3. Pointer vers le fichier dans public/
          style={{ width: '400px', height: 'auto', marginBottom: '20px' }} // Ajustez la taille ici
        />

        {/* Le sous-titre optionnel */}
        <p style={{ fontFamily: 'sans-serif', fontSize: 32, color: '#94A3B8', marginTop: 10 }}>
          Rankez plus haut, plus vite.
        </p>
      </div>
    </AbsoluteFill>
  );
};