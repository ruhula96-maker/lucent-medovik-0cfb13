import admin from 'firebase-admin';

const serviceAccount = JSON.parse(process.env.FIREBASE_SERVICE_ACCOUNT_KEY);

if (!admin.apps.length) {
  admin.initializeApp({
    credential: admin.credential.cert(serviceAccount)
  });
}

const db = admin.firestore();

export default async (req, res) => {
  res.setHeader('Access-Control-Allow-Origin', '*');
  try {
    const snapshot = await db.collection('products').get();
    const products = snapshot.docs.map(doc => ({ id: doc.id,...doc.data() }));
    res.status(200).json(products);
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
};
