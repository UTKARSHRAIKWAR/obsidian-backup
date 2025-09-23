frontend - import axios from "axios";
const API = axios.create({
baseURL: import.meta.env.VITE_API_BASE_URL,
withCredentials: true,
});
export default API;


frontend - use of API component
const {user} = await API.post({})


backend - const corsOptions = {
origin: "https://urlshortmini.netlify.app", // Replace with your frontend's origin
credentials: true,
};
app.use(cors(corsOptions));
W