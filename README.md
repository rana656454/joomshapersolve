# joomshapersolve

import { Suspense, useState, useEffect } from "react";

const fetchUserProfile = userId => {
	return new Promise(resolve => {
	  setTimeout(resolve, 1000 + Math.random() * 1000);
	}).then(() => {
	  return {
		name: `User ${userId}`,
		email: `user${userId}@example.com`
	  };
	});
  };



const SuspensefulUserProfile = ({ userId }) => {
	const [data, setData] = useState({});
	useEffect(async () => {
		fetchUserProfile(userId).then((profile) => setData(profile));
	});
	return (
		<Suspense fallback={<h1>Loading User Profile...</h1>}>
			<UserProfile data={data} />
		</Suspense>
	);
};
const UserProfile = ({ data }) => {
	return (
		<>
			<h1>{data.name}</h1>
			<h2>{data.email}</h2>
		</>
	);
};
const UserProfileList2 = () => (
	<>
		<SuspensefulUserProfile userId={1} />
		<SuspensefulUserProfile userId={2} />
		<SuspensefulUserProfile userId={3} />
	</>
);

export default UserProfileList2;
